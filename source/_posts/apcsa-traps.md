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
此文只包含对于本人来说死记硬背能提升做题速度的知识点，所有写过的代码见 [APCSA](https://github.com/ApolloZhu/APCSA)

## 测试

> Q: A large Java program was tested extensively, and no errors were found. What can be concluded?

> A: **The program may have bugs.**

<!-- more -->

Even after you tested --

- values from each range
- all boundary values
- values outside boundaries

## 整数除法

```java
System.out.print(3/4); // 1
```

## 四舍五入

强转 int 直接 truncate 小数部分，不分正负

```java
int round(double num) {
    return (int)(num + (num > 0 ? .5 : -.5));
}
```

----

# 常识

## 请在答案中使用这个函数的 flag

```java
public aMethod()
{ /* implementation not shown */ }
```

## 随机数

`Math.random()` 返回 [0,1) 任一值

```java

E pick(E[] array) {
    return array[(int)(Math.random()*array.length)];
}
E pick(List<E> list) {
    return list.get((int)(Math.random()*list.size()));
}
```

### start - end 之间随机整数

```java
int random(int start, int end, boolean includeEnd) {
    return (int)(Math.random()*(end-start+(includeEnd?1:0))+start);
}
```
