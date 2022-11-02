# 其他

## 相关教程

关于iOS开发相关的内容，比如iPhone开发等，已整理至另外独立教程：

[苹果相关开发总结 (crifan.org)](https://book.crifan.org/books/apple_develop_summary/website/)

另外，和当前iOS开发总结的相关教程：

* [移动端APP开发总结 crifan.org](https://book.crifan.org/books/mobile_app_summary/website)

其中也有一部分的，和Android开发对应的，也属于iOS开发的内容，供参考。

## iOS开发经验

### 不要在启动页去检测新版本，可以改在登录页去检测新版本

之前做了个企业版的iOS的App

在启动页去检测新版本，所以需要访问网络

但是遇到一些情况是：

有2个`iPhone 6 Plus`的手机，`iOS`版本都是`10.2.1`左右

在首次安装后，即使已经去信任该app了

但是很奇怪的是，默认系统是把该app的网络访问权限禁止掉了

导致这两个6P，首次安装后，卡死在启动页，始终进不去，看不到登录页

解决办法是：

把在启动页需要访问网络的操作（比如检测新版本），改到登录页中，即可避免此问题。

但是目前还有疑惑的是：

为何`iPhone 6 Plus` + `iOS 10.2.1`，首次安装的企业版的app，默认会禁止其网络

而之前的`iPhone 5`、`iPhone 6`等（好像也是`iOS 10.2.1`）却没有出现这类问题。
