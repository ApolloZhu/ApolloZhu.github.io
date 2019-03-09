---
title: 自动深色模式
tags:
  - macOS
  - Swift
  - WWDC18
  - WWDC
categories:
  - 编程
date: 2018-10-28 18:24:04
updated: 2018-11-10 02:04:50
---

我自己开发的 **自动深色模式**（*Dynamic Dark Mode*）基本进入稳定版本了，特此广而告之。希望大家点个星星，顺便帮着宣传宣传。发现 bug 的话，开 PR 提 issue 都行。如果您还会其他语言的话，也欢迎帮忙翻译。链接：[https://github.com/ApolloZhu/Dynamic-Dark-Mode](https://github.com/ApolloZhu/Dynamic-Dark-Mode)

![自动深色模式示意图](https://user-images.githubusercontent.com/10842684/54065607-56c22a80-41f1-11e9-95e6-7100e297d591.PNG)

<!-- more -->

## 开发过程

详情大家可以看 git history，不过我的故事从 WWDC18 说起。

升级了 Mojave 之后发现深色模式竟然不会自动切换，我立马就诞生了写这个程序的想法。每天除了在各种派对里蹭晚饭之外，就是在研究这个。切换深色模式其实就是简单的 AppleScript，我今天在 Apple Store 等着修电脑的时候就背着敲出来了:

```applescript
tell application "System Events"
	tell appearance preferences to set dark mode to not dark mode
end tell
```

不是还有个功能根据屏幕亮度判断是否该启用深色模式么？一开始我以为获取屏幕亮度是件很简单的事情，结果并没有类似于 `UIScreen.main.brightness` 这样的 API。于是 WWDC 的 lab 时间我基本就是在不断地尝试/咨询，可惜苹果的工程师也不清楚。最后还是在 StackOverflow 找到个 [有点复杂的解决方案](https://stackoverflow.com/questions/3239749/programmatically-change-mac-display-brightness)

当然 Apple Engineer 也没有告诉我怎么收听屏幕亮度变化，只告诉我去研究 private framework。当时我就想看看系统偏好设置是怎么做的，于是磨皮擦痒的我就开始同时用键盘和滑条疯狂地调整屏幕亮度。boom，崩溃，Bug Report 跳出来，告诉我研究方向是 `CoreBrightness`。天真的我想着，太好了，直接调用现成的就行了。结果水品太差没分析出个名堂，不过发现了它在屏幕变化的时候会在 `NSDistributedNotificationCenter` 发通知。wow~ ⊙o⊙，问题解决。

前面折腾了这么久，根据日出日落自动定时，我就偷懒直接用了第三方库 [Solar](https://github.com/ceeK/Solar)。不过也有好处，详细了解了各种不同种类的日出日落。实际的定时我也偷了懒，用的是 [Schedule](https://github.com/jianstm/Schedule)。

但是，当我一把沙盒打开，就开始各种扯拐。解决方案也只有两种。当然，你哪种都不能用：

1. 把脚本文件放到 `FileManager.SearchPathDirectory.applicationScriptsDirectory`。有些侥幸上架的 App，比如 [Irvue](https://itunes.apple.com/app/id1039633667)，就是采用的这种方法。这个时候就可以用 `NSUserAppleScriptTask` 来执行这些脚本文件了。苹果爸爸说，不行，你这逃逸沙盒。
2. 配置 `com.apple.security.temporary-exception.apple-events` 为目标对象的 bundle id，也是我现在选择的方法——简洁优雅。当然，就算我给了详尽的解释，仍然被算作了 Sandbox Escape。

又不是逃逸闭包，你™才是 `@escaping` 呢。

## 分发渠道

当然，作为一个良民，我还是希望上 Mac App Store 的，所以才有了上面和 Sandbox 的折腾。但是苹果爸爸明显很是不高兴，具体的过程大家还是去看 [这个记录](https://github.com/ApolloZhu/Dynamic-Dark-Mode/issues/10) 吧，我见着伤心。

所以现在的下载方式是：

1. 直接从 [Release](https://github.com/ApolloZhu/Dynamic-Dark-Mode/releases) 下载 pkg 或者 zip。推荐 pkg，因为不用手动移到“应用程序”文件夹
2. [Homebrew Cask](https://brew.sh/)：`brew cask install dynamic-dark-mode`
3. 之后会考虑加入 Sparkle 来自动更新，不过得等我有空，有空
4. 即使哪天 App Store 被判为垄断（Apple Inc. v. Robert Pepper）的话，也没有希望上架
5. 我要是有机会的话，看看能不能找 Cook 聊聊改 [Apple Developer Program License Agreement 3.3.4 (c)](https://download.developer.apple.com/Documentation/License_Agreements__Apple_Developer_Program/Apple_Developer_Program_License_Agreement_20181019.pdf)

## 市场分析

因为我自己的宣传工作没有做到位，现在 GitHub 上基本上没有什么星星（你们自己点就行了，但千万别去买啊，要不我会被锤的）。现在比较流行的大概是：

- [Dynamic Dark Mode](https://github.com/ApolloZhu/Dynamic-Dark-Mode)：人有的时候就是要脸皮厚一点。不过话又说回来，Google 能直接搜到，星星也还是有些，关键还有 **简体中文** 和其他语言的支持。

- [NightOwl](https://nightowl.kramser.xyz/)：可能是营销做得最好的，也是唯一我百度到的产品。**但是**，我并不喜欢 Google Analytics（根据描述，你的信息至少会被发送一次）。
- [Nocturnal](https://github.com/HarshilShah/Nocturnal)：退出 App 的方法很有意思，感觉哪天可以借鉴一下？
- [sindresorhus/dark-mode](https://github.com/sindresorhus/dark-mode)：命令行工具。作者每个 repo 的星星都不少，是个大神……
- [Gray](https://github.com/zenangst/Gray)：在系统使用深色模式的情况下，配置每个 App 是否使用深色模式。
- [Flux](https://justgetflux.com/) 或 [Shifty](https://github.com/thompsonate/Shifty)：夜间模式+深色模式二合一。

有意思的是，每个 App 的实现都有那么些不一样，包括因为星星太少被我忽略的那些。当然，等苹果出了官方版本之后（他们肯定有计划，Mac App Store 一个都不让通过），我们这些第三方也就基本没啥用了。
