# 约定

iOS中的ObjC中，会看到很多类名是类似于：

最前面是2个大写的字母 + 其他命名

举例：

* **NS**Window
* **CA**Animation
* **NS**WindowController
* **NS**ManagedObjectContext

其中的 `NS`、`CA`等等，都是有对应约定的含义的：

| 前缀 | （所属）框架 |
| -- | --- |
| NS | Foundation (OS X and iOS) and Application Kit (OS X) |
| UI | UIKit (iOS) |
| AB | Address Book |
| CA | Core Animation |
| CI | Core Image |

-》以后再看到类似的类名，就能推断所属的框架=库是哪个了。
