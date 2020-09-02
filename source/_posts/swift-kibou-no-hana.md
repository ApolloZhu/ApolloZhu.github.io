---
title: 不要停下来啊！
tags:
- Swift
- CLI
- tips
categories:
- 编程
date: 2018-11-22 10:47:26
---

{% note info %}
您也可以 [在 bilibili 阅读此文](https://www.bilibili.com/read/cv1557149)，或 [了解标题的出处](https://mzh.moegirl.org.cn/zh-hans/不要停下来啊！)。
{% endnote %}

随着 Swift 对其他操作系统的支持，有的时候我们会遇到程序本身的生命周期在异步函数（比如 `URLSession.dataTask` 的回调）之前就结束了。那要如何才能让程序等到所有代码都执行结束呢？

<!-- more -->

在 Playground 中，我们可以这样：

```swift
import PlaygroundSupport
// 代码...
// 在最后一行加上：
PlaygroundPage.current.needsIndefiniteExecution = true
```

而在普通的命令行程序里（比如 [Srt2BilibiliKit](https://github.com/ApolloZhu/Srt2BilibiliKit) 和最近写的 [拉 B 站粉丝的脚本](https://gist.github.com/ApolloZhu/5031907931fc6bc031a7013bd8075029)），我采用的是：

```swift
import Foundation
// 一般应该都有 ^ 的吧
// 代码...
// 同样也是在文件的最后
RunLoop.current.run()
```

这样，我们的程序就会一直运行下去啦！

{% note danger %}
所以记得用 `exit(EXIT_SUCCESS)` 终止程序！
{% endnote %}
