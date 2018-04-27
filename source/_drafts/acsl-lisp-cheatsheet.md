---
title: ACSL 版 LISP 语法总结
date: 2018-04-26 17:18:44
keywords:
tags:
categories:
- 编程
---

因为没有看过 LISP 官方的文档，ACSL的文档从来都是讲的不明不白，我也只能总结规律，如有不妥，希望大家指正。

LISP 是一种函数式程序设计语言（什么鬼），里面只有两种数据结构——原子和表。所谓的表，其实就是操作符（函数），表，和原子的集合。
> 根据语文老师的说法，新规定要求“和”字前面需要使用逗号。

根据我的总结，数据类型大概可以这样分一下类

- 变量:Object
    - 原子:Atom: atom
        - 数值:Number: 5
    - 表:List:’list
        - 字符串: final String:’string

`NIL` 是一个特例，它既是原子又是表,所以 `’()` 也表示空。

`’`表示在被传入到操作符的是值，列表或是字符串，而不是变量。数字前面不要求加上`’`。这同时也可用 `(quote variable)` 来表示

*之后所有的 LISP 函数都会被用 `Swift` 重现，下面的是可有可无的定义。*

```swift
typealias List = Array<Any>
typealias Atom = Any
```

> 我们假设可以用 `List<T>` 来改写定义。

## 操作符

- ( `QUOTE` variable)

用于返回非变量

```swift
    func QUOTE(variable: Any) ->  Atom{
        return “\(variable)"
    }
```

- ( `SET` variable value)
- ( `SETQ` variable value)

设置 variable 的值为 value

SETQ 的 variable 前面不需要加`’`

```swift
func SET(inout variable: Any, value: Any){
    variable = value
}
```

- ( `ADD` value… )

将所有的 value 相加

```swift
func ADD(value: Number…) -> Number {
    return value.reduce(0, combine: +)
}
```

- ( `EVAL` variable)

感觉和直接打印没设么区别，到时可以明白 quote 的用法。
```swift
func EVAL<T>(variable: T) -> T{
    return variable
}
```

- ( `ATOM` variable)

如果 variable 是原子，则返回 true，否则返回 NIL

```swift
func ATOM(variable： Any) -> Bool?{
        if variable == nil || variable is Atom {
            return true
        }
        return nil
}
```

- ( `REVERSE` list )

将反转表里面的原子的顺序

```swift
func REVERSE(inout list: List){
        list = list.reverse()
}
```

- ( `CAR` list)

返回列表中的第一个项目。如果传入的不是表的话自动 error

```swift
func CAR<T>(list: List<T>) -> T{
        if let item = list.first{
            return item
        } else {
            fatalError()
        }
}
```

- ( `CDR` list)

返回列表中除了第一个之外的项目
```swift
func CDR<T>(list: List<T>) -> List<T>{
        if list.dropFirst().count > 0{
            return Array(list.dropFirst())
        }
        fatalError("NIL")
}
```

- ( `CONS` arg1 arg2)

返回由 arg1 和 arg2 组成的表

```swift
func CONS(arg1: Any, arg2: Any) -> List {
    return Array(arrayLiteral: arg1) + Array(arrayLiteral: arg2)
}
```


## 数学运算符

这个，就不讲解了

```swift
    ADD:    return args.reduce(0, combine: +)
    MULT:   return args.reduce(1, combine: *)
    SUB:    return $0 - $1
    DIV:    return $0 / $1
    SQUARE: return pow($0, 2)
    EXP:    return pow(a,n)
    EQ:     return $0 == $1 ? true : NIL
    POS:    return $0 > 0 ? true : NIL
    NEG:    return $0 < 0 ? true : NIL
```

## 自定义函数

- (DEF name(parameter) alreadyDefinedFunction(parameter))

这个还是举个例子好了

`(DEF SECOND(parms) (CAR (CDR parms)))`

这个可以求表的第二个项

调用的话和以前一样，就是 `SECOND’(1 2))`
