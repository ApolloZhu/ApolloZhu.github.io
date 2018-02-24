---
mathjax: true
title: 一团糟的回锅肉丁！
date: 2018-02-24 10:18:48
keywords:
- 哈希
- Hashtable
- HashMap
- HashSet
- TreeMap
- TreeSet
- APCS
- Advanced Computer Science AB
tags:
- Java
categories:
- 编程
---

不，不，我们要讨论的是 hash，哈希在编程中的运用，毕竟所有的 Java 对象都是 [`Equatable & Hashable`](https://github.com/apple/swift-evolution/blob/master/proposals/0185-synthesize-equatable-hashable.md) 的，而且和 Swift 一样没带上 [`Comparable`](https://github.com/apple/swift-evolution/blob/master/proposals/0185-synthesize-equatable-hashable.md#support-for-comparable) 一起玩。

<!-- more -->

## 查找表和哈希表

为了 $O(1)$ 搜索而存在的数据类型，无序遍历。Look up table 的数组为了放下所有的值，会浪费很多的空间，而且是各占一个位置。而 hash table 则是把 hashcode 转换为合法的数组索引，更节省空间。不过这也给哈希表带来了最大的问题：collision。

## 解决冲突（碰撞）

两个不“相等”的对象被安排到同一个索引的时候，我们就需要考虑如何 resolve collision。

### 开放定址

Open addressing 就是可以占别人的位置，其中一种占的方式是线性的 linear probing，也就是当前的没了就占下一个空位。但这种方式是有弊端的。一是占的越多，就会产生 filled sequence，一连串都被占了。这种 cluster 就会导致发生冲突的可能性变得更高，于是最后就喜闻乐见地变成 $O(n)$ 了。二是得用 soft delete，删除的时候要留个占位的，否则搜索就全乱了，因此占位的对象太多的时候也需要 rehash。

还有一种 quadratic probing，没了就占往后数 $i^2$ 的空位。这种方式对 load factor 要求很高，负载不能超过 50%，否则很可能会找不到空位。那就扩容量呗！先不说会降低遍历效率，关键在于 rehash 的时候对数组长度还有要求……目前网络上的描述大多不完善（准确），所以现在正在研究中，要是捣鼓得出结果的话之后会单独讨论。

### 聚集

这类方法是把每个空位视为一个 bucket，也就是存放多个值的集合。用二维数组实现会浪费太多空间，不推荐。`ArrayList` 和 `LinkedList` 会稍微好些，即使负载大于 100% 的时候性能也不会掉太多。但极端情况下还是会导致查找变成 $O(n)$，所以如果可以比较对象的话，用 BST 能保证 $O(log n)$ 的搜索。

## Java 里哈希值的运用

Java 里的 `TreeSet` 比较坑，因为内部是基于 `TreeMap` 的二叉搜索树实现的，所以要不得有个 `Comparator`，要不类型本身得是 `Comparable`，但是构造器并没有对泛型进行限制，所以不满足条件会直接抛 `ClassCastException`。

相比之下 `HashSet` 里的 `HashMap` 是基于 `hashCode()` 然后 `equals(Object)` 进行的判断。记住别只是重载个 `equals(this.class)`，因为对泛型的类型擦除会导致运行时直接去找 `equals(Object)`。

顺便提下 `Hashtable`，和 `HashMap` 的区别就是 `synchornized`，不接受 `null` 值，继承了被抛弃的 `Dictionary`，总结一下就是没有被钦定。

## 潜规则

所以为了正常使用这些基于哈希值的数据类型，除了别搞幺蛾子之外，存在着 hashcode contract：

- `compareTo` 返回 `0` 时 `equals` 返回 `true`，反之亦然
- 同一个对象在状态未变的情况下，该次程序运行期间哈希值相同
- 同时 `@Override` `equals` 和 `hashCode`，使“相同”的对象具有相同的哈希值
- 相同的哈希值并不代表两个对象“相等”

----

顺便说一句，《算法图解》（*Grokking Algorithms*）并没有想象中的那么实用（有趣且全面），不是很推荐。但不论怎么说，[作者](https://github.com/egonSchiele) 的艺术作品还是可以的。
