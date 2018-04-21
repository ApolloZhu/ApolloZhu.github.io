---
title: WWDC17 Lab 汇总
date: 2017-06-20 12:32:07
tags:
- WWDC17
- WWDC
- tips
- Swift
- bash
- macOS
- Xcode
categories:
- 编程
---

## Swift

### 入门

The Swift Programming Language
Start Develpoing iOS Apps (Swift)
App Development with Swift
CS193p
各种苹果文档

## Swift Playgrounds
Localization: lost of callout effect for `- Experiment`, `- Important`, etc.
- File radar please.

Open playground book with Xcode? How Apple compose a playground book?
- Shared Code Base within Xcode project. Some python tool


## Swift

`#selector` not working within lazy property
- Forgot to ask

### 弱引用数组

```swift
public struct Weak<T: AnyObject> {
    public private(set) weak var pointee: T?
    public init(_ pointee: T) {
        self.pointee = pointee
    }
}

public func weak<T: AnyObject>(_ pointee: T) -> (() -> T?) {
    return { [weak pointee] in return pointee }
}

public func weak<T: AnyObject>(_ closure: () -> T) -> (() -> T?) {
	return { [weak pointee = closure()] in return pointee }
}
```

## Xcode 9

### 终止 Xcode Server

```bash
sudo xcrun xcscontrol --reset
```

## Swift Playground

iOS App + playground share

bug report -> feature request
editing experience
edit files
convert format
syntax highlighting


## HealthKit

AnchoredQuery 取代 SampleQuery

## CALayer Session

shimer: gradient start/end point animation

dash phase for waiting

timeoffset for aligning animation

## Metal

metalbyexample.com

### shaders

- metal programming guide
- metal language specification

----

## kernel 内核

### 单线程 100% CPU

```bash
dd if=/dev/zero of=/dev/null
```

### 动态库加载

dyld

## 美工

### Fox 的模型制作

3dsmax

## Passbook layout

implement layout first
scroll view

- view controllers
- UIKit dynamics
- animation

draw own background view

## blur background image

- metal
- smaller image
- accelerate, vimage
convolution?
- ImageIO local thumbnail

two dimensional linear gradient: small bitmap - stretch image as content of CALayer

Circular gradient view: OpenGL
