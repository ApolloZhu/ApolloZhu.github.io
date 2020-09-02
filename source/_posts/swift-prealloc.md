---
title: 给我占个位置哈
tags:
- Swift
- tips
categories:
- 编程
date: 2018-12-25 13:16:17
---

{% note info %}
您也可以 [在 bilibili 阅读此文](https://www.bilibili.com/read/cv1763556)。
{% endnote %}

不知道大家刷 LeetCode 的时候用的是不是 Swift？会不会在意耗时以及超过了百分之多少的其他解？是否遇到只慢了 4ms 却不知道该怎么才能更快？

<!-- more -->

这个时候可以考虑通过提前分配集合类型的内存，给之后插入的留好位置，避免重新分配。

## Array

因为 `Array` 实现了 `RangeReplaceableCollection`，所以有个 `reserveCapacity(_:)` 方法。虽然没有 LeetCode 的例子，但我们可以用 [EFQRCode](https://github.com/EFPrefix/EFQRCode/pull/51) 来解释一下。

本来代码大概是这样的：

```swift
var array = [Int!](repeating: nil, count: knownLength)
for i in 0..<knownLength {
  array[i] = ...
}
```

但因为 [SE-0054](https://github.com/apple/swift-evolution/blob/master/proposals/0054-abolish-iuo.md) 之后 `ImplicitlyUnwrappedOptional` 没了，所以就变成了：

```swift
var array = [Int]()
for i in 0..<knownLength {
  array.append(...
}
```

就像其他语言的 `ArrayList` 一样，在 `count` 超出 `capacity` 的时候需要重新分配内存。但我们已经知道需要的长度了，这种时候就应该加一句：

```swift
array.reserveCapacity(knownLength)
```

当然，Swift 里 `Sequence` 自带的 `map(_:)` 就是这样做来提高效率的 🥳

## Dictionary 和 Set

这两个都是通过 hash table 实现的，所以都有 `init(minimumCapacity:)` 这个构造器来指定一开始 `_capacity` 的大小。

最著名的例子应该是 [Google 讲解的 Two Sum](https://youtu.be/XKu_SEDAykw) 了：

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
  var complements = [Int, Int](minimumCapacity: nums.count)
  ...
}
```

当然，Set 也差不多。比如 [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/)：

```swift
func numUniqueEmails(_ emails: [String]) -> Int {
  var unique = Set<String>(minimumCapacity: emails.count)
  ...
}
```

这样子写比单纯的 `[Int: Int]()` 或者 `Set<String>()` 会快 4ms 😎
