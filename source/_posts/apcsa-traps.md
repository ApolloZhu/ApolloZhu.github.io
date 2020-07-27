---
title: APCSA 易错点整理
date: 2017-03-20 01:11:28
tags:
- Java
- tips
categories:
- 编程
---

此文只包含对于本人来说死记硬背能提升做题速度的知识点，所有写过的代码见 [APCSA](https://github.com/ApolloZhu/APCSA)

## 测试

> Q: A large Java program was tested extensively, and no errors were found. What can be concluded?

> A: **The program may have bugs.**

<!-- more -->

Even after you tested --

- values from each range
- all boundary values
- values outside boundaries

## 读完 pre/post-condition

这个要是读漏或者读错整个题都会错啊！而且很多时候可以简化代码，不用考虑那么全面。

### 不要杞人忧天

如果你是个非要用空格或是制表符的强迫症患者，这条一定要记住。对于我们这些完美主义者，就算题目给出的答案明显不可能完美地实现，但只要题目中说了 **"implemented correctly"**，请睁一只眼闭一只眼，千万不要和 College Board 计较。

## 整数除法

```java
System.out.print(3/4); // 0
```

## 四舍五入

强转 int 直接 truncate 小数部分，不分正负

```java
int round(double num) {
    return (int)(num + (num > 0 ? .5 : -.5));
}
```

## ArrayList

假设有 `List<E> list`，我们要移除所有等于 `target` 的元素，那需要注意写上绿色的这一行：

```diff
for (int i = 0; i < list.size(); i++) {
    if (target.equals(list.get(i))) {
        list.remove(i);
        // 想一想：如果没有的话会如何？
+       i--;
    }
}
```

或者，我们不自动 `++`：

```java
for (int i = 0; i < list.size(); /*这里什么都不写*/) {
    if (target.equals(list.get(i))) {
        list.remove(i);
    } else {
        i++;
    }
}
```

当然，更简单的方法是反着移除（如果题目允许的话）：

```java
for (int i = list.size() - 1; i >= 0; i--) {
    if (target.equals(list.get(i))) {
        list.remove(i);
    }
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

`Math.random()` 返回 $[0,1)$ 中任一 `double`

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
