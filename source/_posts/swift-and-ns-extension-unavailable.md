---
title: Swift 和 NS_EXTENSION_UNAVAILABLE
date: 2017-06-20 19:30:04
tags:
- tips
- Swift
- WWDC17
categories:
- 编程
---

!['shared' is unavailable: Use view controller based solutions where appropriate instead.](http://wx1.sinaimg.cn/large/9b6450acgy1fgsia3aimjj20n103mq35.jpg)

根据 [App Extension Programming Guide](https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionOverview.html#//apple_ref/doc/uid/TP40014214-CH2-SW6)，有些 API 在 App Extension 中是不允许调用的，其中最典型的一个就是 `UIApplication.shared`。这些方法和属性都由 `NS_EXTENSION_UNAVAILABLE` 这个宏作为标记，在 App Extension 中使用的话 Swift 代码直接无法通过编译（因为程序会直接崩溃），但是因为 Swift 不支持宏定义，所以无法用 `#if` 来判断是否允许调用。虽然 Swift 中也有类似的 `@available`，但是因为只是运行时判断，所以并不能解决无法编译的问题。

目前曲线救国的方法有以下三种<!-- more -->，不过均未考虑对 Objective-C 的兼容，各位请斟酌后使用。

1. 最简单的方法是把需要用到这些 API 的代码作为 extension 放在另一个文件中，只在非扩展的 target 中包含。
2. 或者是修改工程文件，把 `NS_EXTENSION_UNAVAILABLE` 加到扩展 target 的 Build Settings 里的 Swift Compiler - Custom Flags 里。这样就能用 `#if` 判断了。![](http://wx3.sinaimg.cn/large/9b6450acgy1fgslugnclwj20jk05ijs3.jpg)
3. 最后这个方法是在 WWDC17 去 Messages Extension 的 lab 时候想到的，问了下苹果工程师，大概没问题。自己把函数或变量修饰为 `@available(...OSAplicationExtension, unavailable)`，然后内部通过 Key Path 实现。其它 `NS_EXTENSION_UNAVAILABLE` 适用的地方尝试调用会因为 `@available` 无法通过编译，所以只要自己控制好不要在实现的时候乱用就行。完整的例子如下：

```swift
@available(iOSApplicationExtension, unavailable, message: "This is unavailable: Use view controller based solutions where appropriate instead.")
@available(macOSApplicationExtension, unavailable, message: "This is unavailable: Use view controller based solutions where appropriate instead.")
@available(watchOSApplicationExtension, unavailable, message: "This is unavailable: Use view controller based solutions where appropriate instead.")
@available(tvOSApplicationExtension, unavailable, message: "This is unavailable: Use view controller based solutions where appropriate instead.")
open func show() {
    let keyWindow = UIApplication.value(forKeyPath: #keyPath(UIApplication.shared.keyWindow))
    show(in: keyWindow as? UIWindow)
}

open func show(in: UIWindow) { }
```
