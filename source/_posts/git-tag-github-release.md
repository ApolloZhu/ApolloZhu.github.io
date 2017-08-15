---
title: tag 迟到的 GitHub Release
date: 2017-08-15 22:50:35
tags:
- git
- tips
- CLI
categories:
- 编程
---

[CS193P 翻译](https://apollozhu.github.io/Developing-iOS-10-Apps-with-Swift/)了好长的时间了（快四个月了吧，才翻译四集不到？），现在想到通过 release 能够方便通过 RSS 订阅更新，但是 GitHub 只支持最近的几次 commit。怎么办呢？<!-- more -->了解了 GitHub 的 release 其实是基于 git 的标签，那就只有先用 git 打 tag，之后再在 GitHub 上根据 tag 生成 release。

## 创建 tag

```bash
git tag -a <#版本号#> -m "<#信息#>" <#commit#>
```

如果省略 -m 和参数的话，会让你进入 ***vim*** 输入信息的。（`:wq` 退出）
如果省略最后的提交号的话，会 tag 目前的 HEAD。

## 同步 tag

打完标签之后，还需要同步到服务器。普通的 `git push` 是不会同步标签的，需要加个参数：

```bash
git push --tags
```

当然，如果你只想同步部分 tag（比如打错了？），可以只同步某个 tag:


```bash
git push <#tag 名#>
```

----

更详细的使用方法可以参考 [Git 基础 - 打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
