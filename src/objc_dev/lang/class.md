# 类class

TODO：

* 【已解决】iOS的ObjC的类NSURL的函数中获取到实例本身
* MRC ARC 相关
  * 【已解决】iOS的ObjC中数组NSArray类变量是否需要主动free释放内存
* 【已解决】iOS中Objective-C中NSMutableArray初始化是new还是alloc加init

## 创建类的典型逻辑

Object Creation Method Names Must Follow Conventions

创建一个类的几种方法：

举例：

* NSMutableArray
  * `alloc + init`
    ```objc
    NSMutableArray *array = [[NSMutableArray alloc] init];
    ```
  * `new`
    ```objc
    NSMutableArray *array = [NSMutableArray new];
    ```
  * `class factory methods`
    ```objc
    NSMutableArray *array = [NSMutableArray array];
    ```

## 类的声明=Class Declaration

不论是正向的：普通的iOS的代码

还是逆向的：iOS的Logos的hook tweak代码，

写法都是一样的，类似的：

```objc
// Class Declaration
@interface ClassName : SuperClass

- (ReturnType) PropertyOrFunction;

@end
```

举例：

（1）YouTube的Logos的tweak代码

```objc
// Class Declaration
@interface YTWatchController : NSObject
- (id)activeVideoID;
@end

%hook YTWatchController

- (_Bool)isPlaybackVideoPlayingAd{
    _Bool origIsPlaybackVideoPlayingAd = %orig;
    NSLog(@"origIsPlaybackVideoPlayingAd=%d", origIsPlaybackVideoPlayingAd);
    if (origIsPlaybackVideoPlayingAd) {
        NSLog(@"Playing Ads, activeVideoID=%@", [self activeVideoID]);
    }

    return origIsPlaybackVideoPlayingAd;
}
```

（2）iOS的普通的类的代码

```objc
@interface CUICatalog : NSObject

@property(readonly) bool isVectorBased;

-(id)initWithURL:(NSURL *)URL error:(NSError **)error;
-(id)initWithName:(NSString *)n fromBundle:(NSBundle *)b;
-(id)allKeys;
-(id)allImageNames;
-(CUINamedImage *)imageWithName:(NSString *)n scaleFactor:(CGFloat)s;
-(CUINamedImage *)imageWithName:(NSString *)n scaleFactor:(CGFloat)s deviceIdiom:(int)idiom;
-(NSArray *)imagesWithName:(NSString *)n;

@end

void exportCarFileAtPath(NSString * carPath, NSString *outputDirectoryPath)
{
。。。
    CUIThemeFacet *facet = [CUIThemeFacet themeWithContentsOfURL:[NSURL fileURLWithPath:carPath] error:&error];

    CUICatalog *catalog = [[CUICatalog alloc] init];

    /* Override CUICatalog to point to a file rather than a bundle */
    [catalog setValue:facet forKey:@"_storageRef"];
```
