---
title: a == 1 && a == 2 && a == 3
date: 2018-01-21 00:56:17
keywords:
- 面试
- JavaScript
- Swift
tags:
- Swift
categories:
- 编程
---

```swift
if a == 1 && a == 2 && a == 3 {
    print("All three match!")
}
```

这本来是个 JavaScript 的面试题，但这并不能阻止我们研究 Swift 里的解法。

<!-- more -->

{% note warning %}
本文不讨论 Unicode 或藏代码这些方法。
{% endnote %}

## 计算型变量

可能大家最容易想到的，只要每次自加一就好了：

```swift
var _a = 0
var a: Int {
    _a += 1
    return _a
}
```

## 重载运算符

{% note info %}
参数名并不重要，本文采用统一的 `lhs` 和 `rhs`
{% endnote %}

当然可以不改变量，改运算符：

```swift
a = 1
func ==(lhs: inout Int, rhs: Int) -> Bool {
    defer { a += 1 } // 还是自加一
    return !(a != b) // 避免造成递归
}
```

然后就出现了更简单粗暴的

```swift
func &&(lhs: Bool, rhs: Bool) -> Bool { return true }
// 下面这个泛型 T 替换成更准确的类型更保险
func ==<T>(lhs: T, rhs: Int) -> Bool { return true }
```

## `ExpressibleByIntegerLiteral`

这个确实不容易想到，毕竟是反着来，让 1,2,3 被视为相等的，欺骗已经存在的 `==`：

```swift
enum Foo: ExpressibleByIntegerLiteral {
    case bar
    public init(integerLiteral value: Int) {
        self = .bar
    }
}
```

或者我这个有点 C 语系感觉的

```swift
extension Bool: ExpressibleByIntegerLiteral {
    public init(integerLiteral value: Int) {
        self = value != 0
    }
}
```

----

作者虽然中途加了个限制，要求代码同时符合这个运行结果：

```swift
if b == 1 && b == 2 && b == 3 {
    print("All three match!") // 不执行这一条
} else {
    print("All three don't match!")
}
```

但这只要 `a` 和 `b` 不是同一个类型/实现就可以了，没啥影响。而且我们还可以这样掩人耳目：

```swift
let a: Bool = 1, b = 1
```
