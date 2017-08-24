---
title: GitHub's Swift Style Guide
date: 2017-08-23 21:02:25
keywords:
- GitHub
- Swift
- Irony
tags:
- English
- Swift
- git
categories:
- 生活
---

[中文版本](https://zhuanlan.zhihu.com/p/28767790)

When I was cleaning up my GitHub repos and stars, I found [GitHub's style guide for Swift](https://github.com/github/swift-style-guide), and I find this 2nd most starred style guide quite amusing.

<!-- more -->

Despite the fact that Xcode defaults to using 4 spaces for indentation (and we can clearly see the impact by checking [tabs-or-spaces](https://ukupat.github.io/tabs-or-spaces/)), the style guide suggests using tabs instead. I'm totally fine with that, but I can easily tell there are some disagreements among the contributors:

```swift
var myGreatProperty: Int {
	return 4
}

subscript(index: Int) -> T {
    return objects[index]
}
```

But there's more. For now (2017 Auguest 23), there are three [Swift repos](https://github.com/github?language=swift) under GitHub's [main account](https://github.com/github) -- one source, two forks. Well, then let's focus on [SoftU2F](https://github.com/github/SoftU2F), the ONLY Swift repository GitHub actually owns. Isn't it natural for me to expect this repo to follow GitHub's own style guide? But ironically, even SoftU2F is ***NOT*** doing that!

![The Front-End Conftocat on GitHub Octoex](https://octodex.github.com/images/front-end-conftocat.png)

In conclusion, seems that GitHub is not interested in styling their Swift code, and thus the GitHub community (or at least the 4k stargazers) has no actual intention to follow GitHub's style guide, too.
