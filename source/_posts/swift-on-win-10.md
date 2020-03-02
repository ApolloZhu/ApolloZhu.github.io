---
title: 在 Windows 10 上跑 Swift
date: 2017-09-22 14:50:26
keywords:
- Swift
- Windows 10
- Ubuntu
- WSL
tags:
- Swift
- Windows
categories:
- 瞎捣鼓
---

抛开大多数连 Swift 是什么都没有听说过的人，知道 Swift 的人大多都觉得它只能用于 iOS 开发，其实不然。Swift 在 15 年底就支持了 Windows 和 Android，不过因为编译过程过于复杂，所以没有掀起太大的涟漪；反倒是 2017 年夏天的时候微软宣布把 Ubuntu 搬进 Windows 让 Swift 有了大显身手的机会。

<!-- more -->

## 配置

Windows Subsystem for Linux (WSL) 是这一切的基础，所以我们需要在 Windows 10 上安装 Ubuntu，然后用 bash 安装 Swift 编译器。可惜的是 WSL 并不支持 Swift 的交互式解释器（REPL），尽管如此缺依然要求你有 **版本 1607 及以上 的 64 位 Windows 10**（可以在 *设置 > 系统 > 关于* 中查看）。

## 步骤

我们先要启用适用于 Linux 的 Windows 子系统。以 **管理员** 身份运行 Powershell，输入以下内容。完成后按 `Y` 重启电脑。

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

或者可以在 *控制面板 > 程序 > 启用或关闭 Windows 功能* 中，勾选“适用于 Linux 的 Windows 子系统”，然后点确定。根据提示重启。

重启以后，启用开发人员模式。以 **管理员** 身份运行 Powershell，输入以下内容：

```powershell
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowDevelopmentWithoutDevLicense" /d "1"
```

或者可以在 *设置 > 更新和安全 > 针对开发人员* 中，选择 “开发人员模式”

最后安装 Ubuntu，建议用 ***非*管理员** 模式运行 Powershell，输入以下内容。完成安装之后，输入 `bash` 进入 Ubuntu 系统。

```powershell
lxrun /install /y
```

以上方法是懒人配置，如果想自定义，请输入 `bash`，然后根据提示配置。

最后安装 Swift。为了简化步骤，借鉴了喵神借鉴 Vapor 来的代码，稍微修改后做了个自动安装的脚本。输入：

```bash
eval "$(curl -sL https://raw.githubusercontent.com/ApolloZhu/script/master/swift/install/4)"
```

看到“✅ Done”，下一行写着 Swift 版本号的话，那就大功告成了！如果想自定义安装步骤，可以把上面的 [bash 脚本](https://github.com/ApolloZhu/script/blob/master/swift/install/4)稍微改改。

## 接下来呢？

因为不支持 REPL，所以只有写好了程序再编译。怎么才能写程序？ <del>写程序是不可能的，这辈子都不可能写程序的</del> 因为 Ubuntu 是 Windows 的子系统，所以文件是两边都可以访问的，也就是你可以在 Windows 上把程序写好了，再在 Ubuntu 里运行。不过没了 Xcode，你们用什么编辑器就都随意吧。

玩腻了要卸载 Ubuntu？执行命令

```powershell
lxrun /uninstall /full /y
```

## 参考

- [Swift 支持的平台](https://github.com/apple/swift/blob/master/lib/Basic/LangOptions.cpp)
- [WSL 安装](https://msdn.microsoft.com/en-gb/commandline/wsl/install_guide)
- [暂不支持 Swift 交互式解释器](https://github.com/Microsoft/BashOnWindows/issues/688)
- 本文在 B 站 [cv18127](https://www.bilibili.com/read/mobile/18127)
