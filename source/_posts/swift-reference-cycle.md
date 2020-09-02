---
title: guard let self = self else { return }
tags:
- Swift
categories:
- 编程
date: 2019-05-20 01:01:48
---

{% note info %}
您也可以 [在 bilibili 阅读此文](https://www.bilibili.com/read/cv2719977)，或者了解 [白学](https://zh.moegirl.org.cn/白学)
{% endnote %}

没错，这段代码的意思就是“老子就是老子”！让我们一起来看看这段莫名其妙的代码究竟有什么奥秘。

<!-- more -->

首先，它是要解决什么问题呢？当多个对象之间相互持有强引用的话，那么谁都无法从中被释放，这是非常糟糕的情况，我们通常称为 ~~[修罗场](https://www.bilibili.com/video/BV1J4411j7gg)~~ 引用循环。那么在 Swift 里的引用循环是什么样的呢？我们可以看看 Memory Graph（Xcode 自带）所创作的艺术作品：

[![MaterialKit 使用 KVO 强引用视图导致引用循环](https://cloud.githubusercontent.com/assets/10842684/19703440/d77df2f4-9ad1-11e6-9531-2ddd1271d40c.png)](https://github.com/LiulietLee/Pick-Color/issues/2)

还有更夸张的：

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">Sometimes you have small memory leaks, sometimes you accidentally create a retain-cycle fractal universe <a href="https://t.co/fA9KylCzqo">pic.twitter.com/fA9KylCzqo</a></p>&mdash; Oskar Groth (@oskargroth) <a href="https://twitter.com/oskargroth/status/1106693954991476745?ref_src=twsrc%5Etfw">March 15, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## 为什么会变成这样呢？

Swift 中的引用方式有三种：强引用、弱引用（`weak`）和无主引用（`unowned`）。具体的可以看《The Swift Programming Language》里关于 [Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)（[自动引用计数](https://swiftgg.gitbook.io/swift/swift-jiao-cheng/24_automatic_reference_counting)）的介绍，不过简单总结一下的话就是

- **强引用**：默认，抓着其他对象不放，直到自己的生命结束
- **弱引用**：佛系引用，对象在就有值，对象没了就是 `nil`，所以必须是可选类型
- **无主引用**：强制解包的弱引用，对象在一切安好，对象没了直接崩溃

所以当两个对象互相持有对方的强引用的时候，比如下面文件夹和文件的例子：

```swift
class Folder {
  var files = [File]()
}

class File {
  var parentDirectory: Folder?
}

let folder = Folder()
let file = File()

file.parentDirectory = folder
folder.files.append(file)
```

就会导致大家都等着对方先放手，直到天荒地老（程序耗尽内存停止运行），谁也逃不掉。

## 我怎么知道有没有引用循环？

最简单的方法：能不写 `self` 的时候就不写，当 Xcode 提示必须加上 `self`，比如下面这个错误示范里面这样，那就是可能会造成引用循环：

```swift
class SomeTableViewController: UITableViewController {
  // ...
  DispatchQueue.main.async {
    tableView.reloadData()
//  ^ Reference to property 'tableView' in closure requires explicit 'self.' to make capture semantics explicit. 
//  Fix-it: Insert 'self.'
  }
  // ...
}
```

但是，上面那个文件系统的例子导致的引用循环就不能通过这种方式发现，所以我们需要用到 Memory Graph。运行你的程序之后，点击这个按钮就能看到对象之间的引用情况：

[![分隔线后第二个按钮，三个圆圈被两条线连成三角形](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/debugging_with_xcode/Art/debug-bar-debug-memory-graph_2x.png)](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/special_debugging_workflows.html#//apple_ref/doc/uid/TP40015022-CH9-DontLinkElementID_3)

有时甚至看 memory graph 也没办法搞明白究竟是什么导致了内存泄漏，可以看看 [CS193p](https://cs193p.sites.stanford.edu) 或 [WWDC](https://developer.apple.com/videos/developer-tools/performance) 了解如何使用 Instruments 这个复杂但是功能强大的软件。

## 我知道错了，我下次还敢？

最偷懒的解决方式就是，每次 Xcode 让你加 `self` 的时候就听它的，但你还另外在闭包的最开始加上这行全是关键字的代码：

```swift
[weak self] in guard let self = self else { return }
```

它会先弱引用 `self`，然后确认我们能够暂时强引用 `self`，在闭包运行结束之后就释放对 `self` 的引用，这样就能解决大部分闭包导致的引用循环了！不过，如果出现多层闭包嵌套（甚至是 callback hell）的情况呢？

```swift
// 很常见的代码，后台下载数据
URLSession.shared.dataTask(with: URL(string: "AZ.png")!) {
  (data, response, error) in
  let image = UIImage(data: data!)
  DispatchQueue.main.async {
    // 主线程更新 UI
    [weak self] in guard let self = self else { return }
    self.imageView.image = image
    UIView.animate(withDuration: 1) {
      self.imageView.alpha = 1
    }
  }
}
```

这样写是正确的吗？并不，因为 `async` 的闭包已经把 `self` 转为了强引用，所以 `animate` 的闭包用的 `self` 也是强引用的，有可能造成引用循环。所以应该改写成这样：

```diff
URLSession.shared.dataTask(with: URL(string: "AZ.png")!) {
  (data, response, error) in
  let image = UIImage(data: data!)
  DispatchQueue.main.async {
    [weak self] in guard let self = self else { return }
    self.imageView.image = image
    UIView.animate(withDuration: 1) {
+     [weak self] in guard let self = self else { return }
      self.imageView.alpha = 1
    }
  }
}
```

你以为这样就完了？naïve！因为 [SR-3805](https://bugs.swift.org/browse/SR-3805) 里提到的编译器的行为（或者叫做一般人不知道的坑），为了能够让内层的闭包弱引用 `self`，外层的闭包默认强引用了 `self`，也就是说 `dataTask` 里的 `self` 是强引用。所以（非常容易不小心写错的）正确写法是：

```diff
URLSession.shared.dataTask(with: URL(string: "AZ.png")!) {
- (data, response, error) in
+ [weak self] (data, response, error) in
  let image = UIImage(data: data!)
  DispatchQueue.main.async {
-   [weak self] in guard let self = self else { return }
+   guard let self = self else { return }
    self.imageView.image = image
    UIView.animate(withDuration: 1) {
      [weak self] in guard let self = self else { return }
      self.imageView.alpha = 1
    }
  }
}
```

{% note warning %}
注意 `[weak self]` 是在最外层的闭包声明的，但 `guard let` 是在第二层闭包才有。
{% endnote %}

最后想说的是，上面都只是为了示范，其实如果可以的话，就一直用 weak self 也是没有问题的。避免了 guard let 也避免了很多麻烦，不过并不是什么时候都能这么用的：

```swift
URLSession.shared.dataTask(with: URL(string: "AZ.png")!) {
  [weak self] (data, response, error) in
  let image = UIImage(data: data!)
  DispatchQueue.main.async {
    self?.imageView.image = image
    UIView.animate(withDuration: 1) {
      self?.imageView.alpha = 1
    }
  }
}
```

## 等等，刚才的三角关系呢？

稍微有些复杂，因为我们期望的是当文件被移除的时候文件夹不会死拽着不放，所以我们需要数组能够存储弱引用。因此，我们需要引入一个新的类型来包装一下：

```swift
class WeakBox<T: AnyObject> {
  weak var value: T?
}

class Folder {
  var files = [WeakBox<File>]()
}
```

这样，当一个文件（File）实例消失之后，其文件夹的数组里只会留下包装用的 `WeakBox`（`value` 自然是 `nil`）。

但其实更常见的问题是不正确的代理模式导致引用循环（比如 View 和 Controller 之间的通信）。下面这个例子中，根目录（root）和文件系统（fileSystem）之间存在循环引用：

```swift
protocol FolderWatcher {
  func folderDidChange(_ folder: Folder)
}

class Folder {
  var delegate: FolderWatcher?
  // ...
}

class FileSystem: FolderWatcher {
  let root = Folder()

  init() {
    root.delegate = self
  }
}
```

而正确的代理模式应该弱引用 delegate：

```diff
- protocol FolderWatcher {
+ protocol FolderWatcher: AnyObject {
...

class Folder {
- var delegate: FolderWatcher?
+ weak var delegate: FolderWatcher?
```

注意新增的 `AnyObject` 要求，因为只有类的实例能够被引用，值类型是不行的哟～
