---
title: 我去，Mac 打不开了。怎么办？
date: 2018-04-26 17:34:08
tags:
- macOS
- tips
categories:
- 瞎捣鼓
---

Mac 刚开机就黑，根本进不了系统？要简单的话那肯定是预约苹果的 Genius Bar，只要不换零件都是免费的。但在等待的期间，我觉得还可以先尝试抢救一下。

<!-- more -->

## [安全模式](https://support.apple.com/HT201262)

开机时按住 `shift` 键进入安全模式，系统会尝试修复问题，不过这只适用于由于软件导致的问题。

## [恢复模式](https://support.apple.com/HT201314)

开机时同时按住 `command` 和 `r` 键进入恢复模式。这个时候有 Time Machine 备份那肯定是最好的，直接恢复备份就行了。没有的话可以先尝试[使用磁盘工具修复磁盘](https://support.apple.com/HT201639)。

到了最后是在没有办法的时候，重装系统也是从这里。***不过在此之前，请先尝试其他方式，不能放弃治疗。***

## [单用户模式](https://support.apple.com/HT201573)

开机时同时按住 `command` 和 `s` 键。你会看到黑底白字开始刷屏，不需要担心，等它停下就好了。接着我们就可以开始用 [fsck](https://support.apple.com/HT203176) 来尝试修复磁盘工具没法修复的问题。输入并回车

```bash
fsck -fy
```

希望你看到的不是类似于 `disk0s2: I/O error` 一类的错误信息。但要是不凑巧的话，你还可以再碰碰运气。输入并回车：

```bash
fsck_hfs FY /dev/disk0s2
```

{% note warning %}

## 但还是没修好

尝试下其他[可以在开机时用的组合键](https://support.apple.com/HT201255)，仍然不行的话就只有考虑把电脑里还没有备份的文件拷贝出来了。具体操作请参考 [这篇文章](https://apollozhu.github.io/2016/04/10/backup-dead-mac/)。

{% endnote %}
