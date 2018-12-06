---
title: 本地化与国际化
tags:
  - tips
categories:
  - 编程
date: 2018-11-22 15:59:21
---

全球化（Globalization/G11N）包括了三个部分：

- 国际化（Internationalization/I18n）：使程序能被本地化
- 本地化（Localization/L10N）：让内容适应本地市场，文化习俗等
- 翻译（Translation/T9N）

连在一起就成了 `GILT`。也是，做好了算是给产品镀金，没做（好）就应该感到内疚。

> 讲谐音梗是要扣钱的！

那么，具体我们应该怎么操作呢？

<!-- more -->

## NSLocalizedString

```swift
func NSLocalizedString(
  _ key: String,
  tableName: String? = default,
  bundle: Bundle = default,
  value: String = default,
  comment: String
) -> String
```

我们来一个个分析

|参数|作用|
|-:|--|
|key|唯一标识符（仅限 ASCII），没有 value 时的默认值|
|tableName|为了避免重复/更加整洁，保存在 `tableName`.strings 文件里。如果以 `.nocache` 结尾的话，里面的字符串不会被 Bundle 缓存（具体有啥用值得研究）。默认是 Localizable.strings。|
|bundle|默认是 `main`，写框架的话可以用 [`Bundle(for: AnyClass)`](https://developer.apple.com/documentation/foundation/bundle/1417717-init)|
|value|没有翻译时的默认值，实际操作发现并不适合填写（导出其他语言时候并没有作为默认值）|
|comment|用来 **认真** 解释使用情形，虽然不负责任的工程师们一般都不填（确实很难写就是了）|

大概使用起来是像这样：

```swift
alert.informativeText = NSLocalizedString(
  "Location.notAvailable",
  comment: "Failed to attain user's location for sunset/sunrise calculation."
)
```

### key 的选择

翻译有趣的地方在于同一个词/语句会有不同的翻译，仅仅是最简单的 yes/no/okay 都有/需要很多种翻译。所以使用值本身作为 key 是非常不合理的，那么我们应该怎么做呢？

就像 [LINE SDK](https://github.com/line/line-sdk-ios-swift/blob/6637eabd3bceb0a273fa17ba67360167b5a1a233/LineSDK/LineSDK/Login/LoginButton.swift#L160) 一样，通常的做法是使用命名空间：

```swift
buttonText = NSLocalizedString("linesdk.login.button.login"...
```

这样既能保证唯一性，又能让我们一眼看出是否翻译，还提供了上下文，是不错的选择。

![胡清阳同学提供的 bug 显示了苹果选择的 key 也用了命名空间](https://user-images.githubusercontent.com/10842684/48926424-f30f2e00-ee9b-11e8-9f3e-5c55747b73f8.JPG)

不过细心的读者会发现，其实除了命名空间之外，好像并没有规定应该用驼峰，蛇形，还是其他的命名方法。原因很简单，苹果自己也很纠结，不信你看 [App Store Connect](https://appstoreconnect.apple.com/olympus/v1/l10n)。所以大家根据公司要求来就好（没有的话最好现在统一一下）。

## 坑

### 语言概念

单复数
语序：不要拆分字符串

### 长度

double
half

### 从右到左（RTL）

leading, trailing

### 资源文件

颜色
图片

### 格式（Formatter）

DateFormatter, NumberFormatter, etc.

## 参考资料

在此表示，因为引用的内容多/素材本身就没有来源就表示可以不去考究/不列全的人，请务必认真批评！这是在误导学生作弊/被开除！

- [Build Apps for the World](https://developer.apple.com/internationalization/)
- [Internationalization and Localization Guide](https://developer.apple.com/library/archive/documentation/MacOSX/Conceptual/BPInternational/Introduction/Introduction.html)
- [Resource Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/LoadingResources/Strings/Strings.html)
- objc.io 的 [String Localization](https://www.objc.io/issues/9-strings/string-localization/) [中文版](https://objccn.io/issue-9-3/)
- [NSHipster](https://nshipster.com/) 的 [NSLocale](https://nshipster.com/nslocale/)
- [Route 85](https://www.youtube.com/playlist?list=PLOU2XLYxmsIKGQekfmV0Qk52qLG5LU2jO) 的 [Localization 101](https://www.youtube.com/watch?v=87dQNnslltg&list=PLOU2XLYxmsIKGQekfmV0Qk52qLG5LU2jO) 和 [Advanced Localization](https://www.youtube.com/watch?v=6KuMlkbCid8&list=PLOU2XLYxmsIKGQekfmV0Qk52qLG5LU2jO)
