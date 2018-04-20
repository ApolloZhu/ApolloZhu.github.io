---
title: 那些值得一看的 WWDC 视频（持续更新）
date: 2017-08-16 12:55:09
keywords:
- WWDC
- 全球开发者大会
- WWDC 2017
- WWDC17
- 苹果
tags:
- WWDC
- WWDC15
- WWDC16
- WWDC17
- tips
categories:
- 编程
---

为了避免违反苹果的条款，把所有搬运的视频自己删了（之前已经删了一批），免得被苹果工作人员催着删（比如某人录制的 17 年第二天早上奥巴马夫人演讲）。

那就通过此文分享那些有趣/有用的 WWDC 视频吧。

<!-- more -->

## WWDC 2016

### 国际化最佳实践

> 看点：开始小哥打结还以为太紧张说不出话来，结果...

视频：[Session 201: Internationalization Best Practices](https://developer.apple.com/videos/play/wwdc2016/201/)

当时是我在为了一个 [比赛的 App](https://github.com/ApolloZhu/FBLA-2017-NLC) 狂补本地化/国际化，把所有和本地化有关的视频都翻出来了。可以看出苹果一直重视中国市场，工具也越来越好用 (不明白 Route 85 为什么讲这部分的第一期还在推荐用 genstrings)，所以看到这个的时候内心还是很感动的。特别是名字的识别部分，从 ABRecordRef 到 NameComponent，再到现在的大数据自动识别...

看完之后建议看看每年最新的一期，一般都有些新的黑科技。当然如果有去 WWDC 现场不想看 Session，可以在 Lab 直接问 Internationalization & Localization 团队的人有什么新东西（2017 年应该是 stringsdict 模版）。顺便提一下，[Route 85](https://youtu.be/--0Plt3vyt4?list=PLOU2XLYxmsIKGQekfmV0Qk52qLG5LU2jO) 除了上面提到的那一期之外，其他的还是很推荐的。

### 高效地使用 Metal

> 看点：实现斯特拉的魔法ED（误）

视频：[Session 603: Internationalization Best Practices](https://developer.apple.com/videos/play/wwdc2016/603/)

{% note warning %}
建议先学 OpenGL/Metal 再看。
{% endnote %}

[斯特拉的魔法](http://bangumi.bilibili.com/anime/5540)，2016年10月番，ED 的效果很有趣，一直有人常使用各种方法重现。这个视频是讲解 [示例代码](https://developer.apple.com/library/content/samplecode/AdoptingMetalII) 的理论，具体该代码模仿 ED 见 [av7801365](https://www.bilibili.com/video/av7801365/)。

----

## WWDC 2015

### 使用 Xcode 7 进行 UI 测试

> 看点：用户界面测试竟然是这样写出来的？

视频：[Session 406: UI Testing in Xcode](https://developer.apple.com/videos/play/wwdc2015/406/)

看完之后觉得 XCUITest 真的是黑科技。顺便提一下，设置`accessibilityIdentifier` 能够更精准地定位元素，同时 2017 年增加了附件（比如截屏） 的功能。
