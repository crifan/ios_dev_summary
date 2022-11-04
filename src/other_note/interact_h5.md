# 和H5页面交互

在折腾混合app开发时，会涉及到：H5页面开发的混合app，和原生端（此处iOS的）app的交互

此处举例说明：

## iOS原生app和H5的web页面的交互的定义

某APP（主要通过H5的web页面实现）和原生端（iOS/Android）的接口交互的定义

下面简称为：

* 某APP = H5
* 原生端（iOS/Android）= 原生

下面给出相关的接口定义，以及核心代码实现的示例。

功能描述：H5端调用原生的相机去扫码设备的二维码，原生解析得到设备的二维码后返回给H5

### H5调用原生去扫码

* H5端调用`scanDeviceCode()`

```js
    if (window.AppHost !== undefined) {
      console.log(window.AppHost.scanDeviceCode);

      //Native(iOS/Android) scanDeviceCode();
      window.AppHost.scanDeviceCode();
    }
```

* 原生端的具体实现

```objc
// 扫一扫
- (void)scanDeviceCode {
    dispatch_async(dispatch_get_main_queue(), ^{
        if ([PermissionTool cameraPemission]) { // 判断相机权限
            SubLBXScanViewController *scan_vc = [[SubLBXScanViewController alloc] init];
            scan_vc.resultBlock = ^(NSString *idString){
                // oc掉js
                [self scanDeviceCodeCallback:idString];
            };
            [self.webViewController.navigationController pushViewController:scan_vc animated:YES];
        } else {
            [PermissionTool getCameraPemission];
        }
    });
}
```

### 原生端返回扫码结果给H5：`scanDeviceCodeCallback(scannedString)`

* H5端

需要注册js的接口

```js
  componentWillMount() {
    console.log("Header componentWillMount");

    window.scanDeviceCodeCallback = this.scanDeviceCodeCallback;
  }
```

得到结果后进行后续处理：

```js
  //Native(iOS/Android)：scanDeviceCodeCallback(String s);
  scanDeviceCodeCallback(scannedString){
    console.log(`scanDeviceCodeCallback: scannedString=${scannedString}`);

    let deviceCode = this.parseDeviceCode(scannedString);
    console.log(deviceCode);

    if (deviceCode === ""){
      //mannually input, so return empty string
      //so goto input device code page
      route(`${ROUTE_PREFIX.DEVICE_BIND_DEVICE}`);
    } else {
      //scanned out QR code and got device code
      this.checkDeviceCodeBelongToCurCowfarm(deviceCode);

      //for debug
      // route(`${ROUTE_PREFIX.DEVICE_BIND_DEVICE}/${deviceCode}`);
    }
  }
```

* 原生端的具体实现

```objc
// 扫一扫结束
- (void)scanDeviceCodeCallback:(NSString *)idString;

// 扫一扫结束
- (void)scanDeviceCodeCallback:(NSString *)idString {
    
    NSString *jsFunctStr = [NSString stringWithFormat:@"scanDeviceCodeCallback('%@')", idString];
    [self.jsContext evaluateScript:jsFunctStr];
}
```
