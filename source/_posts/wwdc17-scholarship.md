---
title: WWDC17 奖学金项目
date: 2017-04-03 00:26:53
tags:
- Swift
- WWDC17
categories:
- WWDC
---

![](https://cloud.githubusercontent.com/assets/10842684/24595546/7968d9de-1805-11e7-9283-df85393876c5.png)

老实交代，真的是最后几分钟交上去的，紧张的不得了。提交的时候还出了错，让重新登录账号，重新输入信息。那个时候整个人都是慌的，成功提交完了之后人都还在发抖。最后竟然选中了，算是了却了个多年（那个，你又没活那么久）的心愿吧，欣喜如狂。

<!-- more -->

看到 WWDC 的新闻出来了，马上就去看今年 Scholarship 的题目。本来都觉得自己没什么好 App 不准备参加的，结果今年苹果不按套路出牌，不交 app，交 playground。想起来之前有个没有完全实现的 [Swifty Karel](https://github.com/ApolloZhu/Swifty-Karel) 可以用，正好 playground 还能帮我解决编译的问题。

Karel 是斯坦福 [CS106A](https://web.stanford.edu/class/cs106a/) 课程很早开始就用来引导学生学习 Java 的工具，[Karel the Robot Learns Java](https://web.stanford.edu/class/cs106a/resources/karel-the-robot-learns-java.pdf) 一书中有比较全面的介绍。感觉和 Swift Playgrounds 教程几乎没有区别；唯一区别就是，一个是萌萌哒的 3D，一个是像素风的 2D。

## 改进

最后因为时间不够了，其实交上去的 playground 并不算美观，除非 Apple（让我）继续改进，就算选中也不可能拿去展示。我们先来定个小目标，列个[改进清单](https://github.com/ApolloZhu/Swifty-Karel/issues/1)：

- [x] 基本函数介绍
- [x] `Playground.current` 的配置
- [x] 自定义 `ColorScheme`
- [x] `Playground.current` 的导出
- [x] 首页 `"Hello WWDC17"`
- [x] 斯坦福 pdf 里的案例
- [ ] TOC，页眉页脚，LICENSE
- [ ] README

## 忏悔

因为对 SpriteKit 一点也不熟悉，只好用 UIView 和 Timer 来搞动画。其实如果有空可以熟悉一下游戏引擎。之前因为宣誓尽量不开发游戏，加上尝试 SpriteKit 受挫，基本就没动过。现在看来游戏引擎也不是只能开发游戏，还能作为一种展示 UI 的手段。不过改为用 SpriteKit 实现只怕是劳神费力，除非有什么要紧的 bug，否则多半是不会考虑的。

说实话现在还有个不怎么起眼的 bug。因为乱用 Singleton，导致现在 WorldModel 不走 liveView 都展示不出 Karel 来。希望能在写 README 之前解决这个问题。

## 致谢

谢谢初中的徐喜元老师当年破例让我在 NOIP 竞赛班旁听；谢谢老司机 JD 同学领我入门，时刻激励着我不断学习；谢谢父母对我编程的支持。
