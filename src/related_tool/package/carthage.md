# Carthage

TODO：

【已解决】Mac中安装Carthage

---

Carthage包管理器

* 官网
  * [Carthage/Carthage: A simple, decentralized dependency manager for Cocoa](https://github.com/Carthage/Carthage)

## 安装

安装Carthage有3种方式

* 可以下载Carthage.pkg去安装
  * 从
    * Releases · Carthage/Carthage
      * https://github.com/Carthage/Carthage/releases
    * 下载
* 也可以直接用brew去安装：
  * `brew install carthage`
* 也可以用MacPorts：
  * `sudo port selfupdate`
  * `sudo port install carthage`
* 也可以从源码安装
  * `make install`

此处用的是：

```bash
brew install carthage
```

安装后，确认已安装

```bash
 which carthage
/usr/local/bin/carthage
```

查看版本：

```bash
> ll /usr/local/bin/carthage                      
lrwxr-xr-x  1 limao  admin    38B  2 14 13:47 /usr/local/bin/carthage -> ../Cellar/carthage/0.34.0/bin/carthage
```

-> 得知当前安装的版本是：`0.34.0`

## 基本用法

Xcode的项目中，已有配置文件

`Cartfile`

```txt
github "Alamofire/Alamofire" ~> 4.7.2
```

然后再去运行

```bash
carthage update
```

即可更新，安装对应的库。

如果要指定平台，则加上参数：

* 只针对Mac平台
  ```bash
  carthage update --platform macOS
  ```
* 只针对iOS平台
  ```bash
  carthage update --platform iOS
  ```

### 用法举例

```bash
carthage bootstrap --platform ios
```

举例：

```bash
 carthage bootstrap --platform ios
*** Checking out RoutingHTTPServer at "v1.2.2"
*** Checking out YYCache at "1.1.0"
*** xcodebuild output can be found in /var/folders/gt/5868sbcd1jq4rxvryqhy2_1sz8n0s3/T/carthage-xcodebuild.L6l9ZF.log
*** Building scheme "RoutingHTTPServer iOS" in RoutingHTTPServer.xcodeproj
*** Building scheme "YYCache iOS" in YYCache.xcodeproj
```
