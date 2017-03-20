---
title: APCSA 易错点整理
date: 2017-03-20 01:11:28
tags:
	- Java
	- tips
category:
	- 编程
---

本文不定期更新，预计 2017/5/2 停更

## 测试

> Q: A large Java program was tested extensively, and no errors were found. What can be concluded?

> A: **The program may have bugs.**

<!-- more -->

Even after you tested --

- values from each range
- all boundary values
- values outside boundaries


## 四舍五入

强转 int 直接 truncate 小数部分，不分正负

```java
int round(double num) {
    return (int)(num + (num > 0 ? .5 : -.5));
}
```
