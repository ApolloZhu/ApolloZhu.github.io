---
title: 这怎么可能是真的？
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

这本来是个 [JavaScript 的面试题](https://stackoverflow.com/questions/48270127/can-a-1-a-2-a-3-ever-evaluate-to-true)，但这并不能阻止[我们在推特上研究 Swift 里的解法](https://twitter.com/twostraws/status/954709346679754755)。

<!-- more -->

{% note warning %}
本文不讨论 Unicode 或藏代码这些方法。
{% endnote %}

## 计算型变量

这可能是大家最容易想到的，只要每次自加一就好了：

```swift
var _a = 0
var a: Int {
    _a += 1
    return _a
}
```

## 重载运算符

{% note info %}
参数名并不重要，所以本文采用统一的 `lhs` 和 `rhs`
{% endnote %}

当然除了改变量之外，改运算符也是一种思路：

```swift
a = 1
func ==(lhs: inout Int, rhs: Int) -> Bool {
    // 不加 `inout` 那 `lhs` 就改为 `a`
    defer { lhs += 1 } // `a = 0` 就不用 `defer`
    return !(lhs != rhs) // 避免造成递归
}
```

然后就出现了更简单粗暴的：

```swift
func &&(lhs: Bool, rhs: Bool) -> Bool { return true }
// 如果 T 已经是 Equatable，那必须得替换成更准确的类型
func ==<T>(lhs: T, rhs: Int) -> Bool { return true }
```

## 遵循新协议

这个有点反着来的感觉，确实不容易想到。我们可以让某种 `Equatable` 遵循 `ExpressibleByIntegerLiteral` 协议，这样 1、2、3 就能被视为和 `a` 是同一个类型的，我们也就可以欺骗已经存在的 `==`，让他们被视为相等的：

```swift
enum Foo: ExpressibleByIntegerLiteral {
    case bar
    public init(integerLiteral value: Int) {
        self = .bar
    }
}
```

或者我这个有点重现 C 语系感觉的：

```swift
extension Bool: ExpressibleByIntegerLiteral {
    public init(integerLiteral value: Int) {
        self = value != 0
    }
}
```

----

楼主中途又加了个限制，要求代码同时符合这个运行结果：

```swift
if b == 1 && b == 2 && b == 3 {
    print("All three match!") // 不执行这一条
} else {
    print("All three don't match!")
}
```

但这只要 `a` 和 `b` 不是同一个类型/实现就可以了，没啥影响。而且我们还可以用类似于这样的方法来掩人耳目：

```swift
let a: Bool = 1, b = 1
// 上面的 `b` 还是 `Int`
```

如果你还有其他的姿势，不妨在下面，到 [bilibili](https://h.bilibili.com/1789925)，或者去 [推特](https://twitter.com/twostraws/status/954709346679754755) 上回复。
