---
title: 令人脸扁的 macOS 程序图标替换
date: 2017-12-07 18:30:13
keywords:
tags:
categories:
- 编程
---

毕竟是亲儿子，用 Swift 实现运行时替换程序图标，是舒服得脸扁；不过用 Java 实现，那可是恼火得脸扁。

<!-- more -->

## 如果你用 Swift

用 Swift 在 macOS 上把图标替换为另一张图片：

```swift
NSApp.applicationIconImage = #imageLiteral(resourceName: "图标的名字.png")
```

如果要设置为 `NSView` 的话，可以用下面的方法：

```swift
// 如果有需要可以获得图标的大小：
let size = NSApp.dockTile.size
NSApp.dockTile.contentView = <#T##作为图标的 NSView##NSView#>
NSApp.dockTile.display()
```

{% note primary %} `<##>` 是 Xcode 使用的占位符的格式，大家可以尝试下。 {% endnote %}

## 如果你用 Java

你可能会说为什么不用 `JFrame::setIconImage` 或者 `add` 到 JavaFX 的 `Stage.getIcons()` 里——naïve。虽然他们不考虑 Mac，但我们为他们着想，在 Java 彻底提出解决方案之前，为了兼容其他平台，我们使用反射实现：

```java
try {
    Class NSApplication = Class.forName("com.apple.eawt.Application");
    Method sharedApplication = NSApplication.getMethod("getApplication");
    Object shared = sharedApplication.invoke(NSApplication);
    Method setApplicationIconImage = NSApplication.getMethod("setDockIconImage", java.awt.Image.class);
    setApplicationIconImage.invoke(shared, /*作为图标的  Image*/);
} catch (Throwable ignored) { }
```

虽然错的明明是他们，但上面提到的方法在 Java 9 （没事干不要用 Java 9）下还是会被警告的，因为[之后会有解决方案](http://openjdk.java.net/jeps/272)。顺便提一句，虽然因为上面的例子肯定要 try-catch 所以没有必要，但可以这样判断是 Mac 系统：

```java
System.getProperty("os.name").toLowerCase().contains("mac")
```

----

有哪里写错了记得让我同时更新 [B 站 cv99301](https://www.bilibili.com/read/mobile/99301)
