---
title: GitHub's Swift Style Guide
date: 2017-08-23 21:02:25
keywords:
- GitHub
- Swift
- Irony
tags:
- Swift
- git
categories:
- 生活
---

[阅读知乎版本](https://zhuanlan.zhihu.com/p/28767790)

昨天在整理 GitHub 上自己和 Star 的项目时，发现了 [GitHub 官方的 Swift 代码规范](https://github.com/github/swift-style-guide)。当时没仔细读，现在重温才发现这个 Star 数排名第二的代码规范实在是有趣。

<!-- more -->

用空格还是 Tab 缩进，这是[一直都在争论的话题](https://ukupat.github.io/tabs-or-spaces/)，统一缩进自然也是代码规范的一部分。Xcode 默认缩进是用四个空格，排名第一的 [raywenderlich 规范](https://github.com/raywenderlich/swift-style-guide) 建议在教程中用两个空格，而 GitHub 的代码规范提倡使用 Tab 缩进。这本来是没有问题的，但可笑的是，好像 GitHub 内部对于怎么缩进好像还存在分歧：

```swift
var myGreatProperty: Int {
	return 4
}

subscript(index: Int) -> T {
    return objects[index]
}
```

> 引用自 GitHub Swift 代码规范，可以看出第一个是 Tab 缩进，第二个是四个空格缩进。

当然，这可能只是写文档比较匆忙，没注意到。那我们看看 GitHub 自己的 [Swift 项目](https://github.com/github?language=swift)。就今天（2017 年 8 月 24 日）而言，GitHub 的 GitHub 账号下有三个 Swift 项目，其中有两个是从 Quick 那边 fork 过来的。我觉得如果 GitHub 强行要求 Quick 遵守 GitHub 的代码规范不是很现实，那就只有看唯一一个 GitHub 实际掌控的项目，也就是 [SoftU2F](https://github.com/github/SoftU2F) 了。按理来说 SoftU2F 应该是要遵守 GitHub 自己的代码规范的吧？可是结果呢？至少缩进是没有遵守的。

[Talk is cheap, I'll show you the code.](https://github.com/github/SoftU2F/search?l=swift)（手动滑稽）

![Smirking Octocat](https://octodex.github.com/images/front-end-conftocat.png)

总而言之，仅从缩进这一点来看，就能看出 GitHub 好像对规范 Swift 代码并没有什么兴趣。这四千多 Star 的人也多半没有按照这个规范来写，只是冲着是 GitHub 写的给个面子罢了。

> ***此文纯属调侃，并无抹黑 GitHub 之意。***
>（不过爱到深处自然黑嘛）
