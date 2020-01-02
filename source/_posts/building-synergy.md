---
title: macOS 下编译 Synergy
date: 2017-03-23 18:06:04
tags:
- tips
- macOS
categories:
- 瞎捣鼓
---

[Synergy](https://symless.com/synergy) 是一款跨平台多电脑共享一套鼠标键盘的利器，可惜正常下载要收费。曾经有段时间可以免费下[内测版](https://symless.com/nightly)，但是现在也不行了。不过作为[开源](https://github.com/symless/synergy)软件，我们可以自己编译。此编译指南**应该**适用于 macOS 10.10 及以上，但是***就算编译正常，还是什么都显示不出来***。

<!-- more -->

## 安装依赖
1. 安装 [Homebrew](https://brew.sh/)
2. 从 Mac App Store 下载 [Xcode](https://itunes.apple.com/us/app/xcode/id497799835)
	1. 打开 Xcode, 选择菜单栏中的 Xcode > Preferences > Locations
	2. 在 Command Line Tools 中选择一个版本
3. 安装 cmake, qt5
```sh
brew install cmake
brew install qt5
```

## 编译

1. 下载 synergy
```sh
git clone https://github.com/symless/synergy.git;cd synergy
```
2. 修正 `ext/toolchain/commands1.py` 文件中的 [bug](https://github.com/symless/synergy/issues/4572) 和 [bug](https://github.com/symless/synergy/pull/5826)
```sh
sed -i "" "s:frameworkRootDir = .*$:frameworkRootDir = \"$(which qmake | sed "s/bin.*$/Frameworks/")\":" ext/toolchain/commands1.py

sed -i "" "s:Contents/Info.plist:Resources/Info.plist:" ext/toolchain/commands1.py
sed -i "" "/self.move/d" ext/toolchain/commands1.py
```
3. 配置参数
```sh
./hm.sh conf -g2 --mac-sdk $(sw_vers -productVersion | sed 's/.\d*.$//') --mac-identity test
```
4. 编译
```sh
./hm.sh build
```
5. 移动到 Applications 文件夹
```sh
mv bin/Release/Synergy.app /Applications/Synergy.app
```
6. 删除原文件
```sh
cd ..;rm -rf synergy
```

----

## 参考

1. [Synergy compile instructions](https://github.com/symless/synergy/wiki/Compiling#Mac_OS_X_1010_and_above)