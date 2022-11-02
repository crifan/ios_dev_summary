# 函数

TODO：

* 【已解决】iOS中ObjC的多参数函数的定义和调用
* 【已解决】iOS中C代码报错：Implicitly declaring library function malloc with type void *unsigned long
* 【已解决】iOS中如何把ObjC提取出通用函数到独立.c文件中供别处调用

---

## Objc函数调用底层实现是`objc_msgSend`

ObjC函数调用：

```objc
[someObj someFunction]
```

对应语法是：

```objc
[receiver message]
```

底层其实是翻译=转换成：

```objc
objc_msgSend(receiver, selector)
```

如果有更多参数，则是：

```objc
objc_msgSend(receiver, selector, arg1, arg2, ...)
```
