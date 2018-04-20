---
title: WWDC18 奖学金指北
date: 2018-03-16 07:55:41
keywords:
tags:
- Swift
- WWDC18
- WWDC
categories:
- 编程
---

> [English Version Here](http://apollozhu.github.io/2018/03/15/wwdc18-scholarships-info/)

之前忘了做自我介绍了。大家好，我是朱智语，去年通过 [Karel the Robot 的 Playground](https://github.com/ApolloZhu/Swifty-Karel/tree/master) 侥幸获得了 2017 年 [WWDC 的奖学金](https://developer.apple.com/wwdc/scholarships/)。关于参加 [WWDC](https://developer.apple.com/wwdc) 本身的介绍，特别是对于国内的朋友们，建议去看看 [喵神的这篇文章](https://onevcat.com/2016/04/first-wwdc/)。本文主要是分享下自己的经验，希望能抛砖引玉，避免其他对此感兴趣的在校学生或者 STEM 组织的成员错过这次机会。

这篇文章会有些长，请大家耐心、仔细地阅读。

<!-- more -->

## 简单的介绍

建议大家仔细阅读 [官方的描述](https://developer.apple.com/wwdc/scholarships/) 以及 [各种条款](https://developer.apple.com/wwdc/scholarships/terms/WWDC18-Scholarship-Terms-and-Conditions.pdf)，但总的来说你需要用 ***英文*** 和 Swift ***独立*** 编写一个有 ***创意*** 和 ***技术水平*** 的 Playground。你需要在北京时间 4 月 2 日早上 8 点之前上交，然后苹果就会在 4 月 21 日通知你是否被选中了！

关于在校学生证明，这个官方的说法是当前的课表或者其他证明在读的文档，加上系主任或者校长的联系信息。STEM 组织我不是很熟悉，但官方的说法大概是成员信息加上组织者的联系信息。文档格式要求 PDF、PNG 或者 JPG，而且交中文的文档也是没问题的，所有语言苹果都认。

## 需要的软件

好消息是，你并不需要苹果的付费开发者账号。而且更优秀的是，如果你有幸得到今年的奖学金，你还能免费成为一年的苹果开发者计划成员。

软件的话，如果你有一台 Mac，你需要 ***从 Mac App Store***（还记得 XcodeGhost 么？）[下载 Xcode](https://itunes.apple.com/app/id497799835)；如果你有一台 iPad, 则需要从 App Store 免费下载 [Swift Playgrounds](https://itunes.apple.com/app/id908519492)；如果你只有 Windows 电脑，那么可以尝试使用虚拟机等（百度 Swift 吧有[介绍](http://tieba.baidu.com/p/3092530089)）。

## 学习 Swift

如果你有 iPad 的话，我强烈建议你尝试下 Swift Playgrounds 里的 “学习编程”，这样你就能在学习 Swift 的同时体验一下 Playground 与普通程序的不同之处。

不过还是有必要更系统的学习 Swift。如果看的懂英文的话，建议去 (i)Books 下载 《[The Swift Programming Language](https://itunes.apple.com/book/id1002622538)》；看不懂英文也没问题？，[这里有中文版](https://www.cnswift.org/)。对于有编程基础的同学，只需阅读 A Swift Tour（Swift 概览）应该就可以掌握这门简单的编程语言了；从未接触过编程的话这个章节可以略读，带着问题阅读 Language Guide（Swift 指南）是个不错的选择。

当然，你完全没有必要读 Language Reference（语言参考）和 Revision History（版本修订历史）。

## 其他要学的

开发 2D 平面游戏的话可以使用 [SpriteKit](https://developer.apple.com/spritekit/)，3D 游戏的话有 [SceneKit](https://developer.apple.com/scenekit/)，[WWDC17 也有讲在 Swift Playgrounds 里使用 SceneKit](https://developer.apple.com/videos/play/wwdc2017/605/)，但我觉得你应该已经略有了解，而且知道去哪里找 3D 模型。但其实 [UIKit](https://developer.apple.com/documentation/uikit) 本身已经能满足大部分的需求。这么短的时间肝 [斯坦福的 CS193p](https://www.bilibili.com/video/av16339375) 是来不及了，但官方还有 [Start Developing iOS Apps (Swift)](https://developer.apple.com/library/content/referencelibrary/GettingStarted/DevelopiOSAppsSwift/)。

其实有时间的话，还应该去看看 [视图控制器的工作原理](https://developer.apple.com/library/content/featuredarticles/ViewControllerPGforiPhoneOS)，进一步了解 [TableView](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/TableView_iPhone/AboutTableViewsiPhone/AboutTableViewsiPhone.html)，以及 [iOS 程序开发](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html)。

## Playground

Playground 里的文档是支持 [Markup](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_markup_formatting_ref/) 的，请避免使用 `print`，并改用这种方式 + `CustomPlaygroundQuickLookable`/`CustomPlaygroundDisplayConvertible` 引导用户。

### Mac, Xcode, 和 Playground

Xcode 里的 Playground 是在 [2014 年的 WWDC 上介绍的](https://developer.apple.com/videos/play/wwdc2014/408/), 并且在 2015 年引入了上面的注释格式来帮助你 [编写更加美观的 Playground](https://developer.apple.com/videos/play/wwdc2015/405/)。 除了 Xcode 里的模版之外，官方还有一个 [简单的案例](https://developer.apple.com/library/content/samplecode/StarterPlaygroundBook/Introduction/Intro.html) 可供参考。如果你去翻 [Swift 的博客](https://developer.apple.com/swift/blog/) 的话，那里也有些没法编译但还是很有趣的 Playground。

### iPad 和 Swift Playgrounds

然后 [2016 年 WWDC](https://developer.apple.com/videos/play/wwdc2016/408/) 就介绍了 Swift Playgrounds 这个 iPad 上的程序，当然 [去年也有更新](https://developer.apple.com/videos/play/wwdc2017/408/)。相比之下，iPad 上的 Playground 有很多优势，比如 [特殊的数据传递方法](https://developer.apple.com/library/content/samplecode/TalkingToTheLiveView/Introduction/Intro.html)，cut scene（用 HTML 编写的“剧情画面”，引入接下来的内容），封面图和术语表等。详情可以参考 [Playground Book Format Reference](https://developer.apple.com/library/content/documentation/Xcode/Conceptual/swift_playgrounds_doc_format/)。

## 个人瞎分析

断网离线判定，不能要求账号，以及 3 分钟时限的规则还在，大家请多注意，但今年不知道为啥提到用苹果新科技这一点，只提了加上图片和音效……不过我估计还是会有不少 [增强现实](https://developer.apple.com/arkit)（你看今年宣传图）和 [机器学习](https://developer.apple.com/coreml) 类的 Playground。

不过说实话，即使可以在说明原因和正确使用 License 的情况下使用第三方开源库，但要交的仍然不能算是是普通的程序。这是你自己写的 Playground，作为可交互式的程序，我建议大家还是尽量体现出 Playground 的特点：

1. 利用 Playground 的各种特性来引导用户，说明接下来要干什么，能达到什么目标
2. 让用户通过编程来主动 [学习新的内容](https://developer.apple.com/videos/play/wwdc2017/416/)
3. 通过有趣的内容激发兴趣，鼓励用户更多地去了解，学习和参与编程
4. ……

去年的 Playground，虽然有不少被采用的并不具备以上特征，但并不能否定他们作为有价值的参考对象。代码的话大部分应该都在 [GitHub 上这个项目里](https://github.com/wwdc/2017)，某Tube 上也有个 [播放列表](https://www.youtube.com/playlist?list=PLl469UE7Uwr0bdon2CvnpxmQs16qu4nkf)（虽然不是很正确但还是希望大家想办法研究，包括 [这个挺不错的](https://www.youtube.com/watch?v=cq_zLMKB-SE) 的投稿）。[App Store 里的故事](https://itunes.apple.com/story/id1358780266) 大家也可以去瞧一瞧，看看过去获奖者的经历。

与此同时，我觉得这个和美国申请大学差不多，硬性条件 Playground 达到某种水平之后就完全靠 "Beyond WWDC" 这篇文章来分高下了。不多，500 词的英语写作，请大家感情丰富，有理有据地描述你如何分享你了解的编程知识以及用对 CS 的热情感化大众。建议大家不要无中生有，还是实事求是的好，不过同一件事情描述的角度不同，体现出来的效果自然是不一样的。大家可以把文章拿去让其他人读一读，参考下大家的意见多修改几遍比较好。

## 最后说几句

你问我难不难，那我肯定说难，不过也并不是说就届不到，实现不了。但也不能说就因为难就去抄，你看去年那个 [2048](https://github.com/wwdc/2017/issues/7) 就被拒了吧。耍小聪明也是不行的，比如交两份啊，尝试黑进苹果什么的都是明令禁止的哦！

如果你还有什么其他问题的话，我都会尽快回答，可能的话我也会更新文章的内容。

最后，祝大家能心想事成，也希望我们能相约六月的圣何塞。
