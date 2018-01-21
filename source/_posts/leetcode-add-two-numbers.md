---
title: LeetCode - 2. Add Two Numbers
date: 2017-11-01 00:10:40
keywords:
tags:
- algorithm
- python
categories:
- 编程
---

本来说 LeetCode 准备全用 Swift，（这道题正常做法 Swift 也行，详见正确答案），但是想偷懒，这个时候只有靠 python 这种适合大数据的才行，毕竟这道题的本质是把两个数相加。

<!-- more -->

> You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.
>
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
> Output: 7 -> 0 -> 8

实际上这就是计算 $342 + 465 = 807$，每个数字分别是倒着写的。所以先 `toInt` 递归把链表转换成整数，然后 `toListNode` 把整数转回链表。但这种不负责任的写法 Swift 会溢出，于是换了 python。

```python
toInt = lambda l: l and toInt(l.next) * 10 + l.val or 0
def toListNode(i):
    base = None
    for c in str(i):
        new = ListNode(int(c))
        new.next = base
        base = new
    return base
class Solution:
    def addTwoNumbers(self, l1, l2):
        return toListNode(toInt(l1)+toInt(l2))
```

`toListNode` 里转字符串完全是不得已而为。我一开始（也是 [StefanPochmann](https://discuss.leetcode.com/topic/14575/python-for-the-win)）用的方法是这样的：
```python
def toListNode(i):
    this = ListNode(i % 10)
    if n > 9:
        this.next = toListNode(i / 10)
    return this
```
有些蹊跷的是，在数字够大的时候，会和正确结果有些出入。原因不明，难不成是除法带来的浮点误差？
