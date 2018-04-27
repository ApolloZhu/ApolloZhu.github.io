---
title: 从坏掉的 Mac 中备份数据
date: 2016-04-10 17:36:38
tags:
- macOS
- tips
categories:
- 瞎捣鼓
---

看到这篇文章的你，请以后记得使用 TimeMachine。然后，只要你的硬盘没有被砸坏一类的，数据还能访问，我这个方法你都可以试试

<!-- more -->

<details>
<summary>要是你对我的电脑出了啥问题感兴趣的话，可以展开来看看，否则就不耽误你时间了。</summary>

我 Boot Camp 分区完准备装 Windows，但不知道为啥失败了，新建的分区还删不掉，所以我决定自己把 Windows 分区删了重新试一遍。这下好了，还是通过 Boot Camp 把镜像写到 32G U盘来安装 Windows，但就打死都不能分区；尝试我自己使用磁盘工具分区，它就提示说错误代码 8。那我就想，会不会安全模式能解决问题？心理窃喜，按住 `shift` 开机，可还没有显示登录界面就直接黑了。没办法，`command` + `R` 进恢复模式修复磁盘，结果它也没辙。恰巧遇到 Genius Bar 偷懒（昨天最晚就开到 17:15，今天不上班），只好开始各种搜索。最后找到了用 FireWire 连接的方法，但关键是哪里又第二台 Mac……

电脑可以换，数据不能丢！仗着还能访问里面的文件，我决定靠自己捣鼓。

> 未来的我：你以后还会把硬盘各种玩坏，把修复过程记下来算是还有自知之明。

</details>

## [目标磁盘模式](https://support.apple.com/HT201462)

如果你能找到另一台 Mac 的话，恭喜你，你只需要再有一条 [FireWire](https://support.apple.com/HT1661)/Thunderbolt/USB-C 的线就可以快速地把数据导出了！连接好两台 Mac，并在你坏掉的电脑开机时按住 `T` 键，就会发现它作为普通的硬盘显示到另一台 Mac 上了！

## 单用户模式

我默认为你已经看过了 [其他抢救措施](https://apollozhu.github.io/2018/04/26/combat-mac-startup-issues/)，正如那里面所说的，开机时同时按住 `command` 和 `S` 键进入单用户模式，等待满屏飞过奇怪的代码。

{% note success %}

之后我们将开始敲命令。如果不小心执行了奇怪的命令，你可以通过按下 `control` 和 `C` 键来终止该命令。

{% endnote %}

## 驱动 USB

在插入U盘之前，我们先先确认已经存在的磁盘。输入：

```bash
ls -l /dev/disk*
```

你会看到例如这样的输出：

```
disk0
disk0s1
disk0s2
```

接着我们插入 USB 设备然后再输入一次

```bash
ls -l /dev/disk*
```

就可以看到多出来的磁盘了：

```
disk0
disk0s1
disk0s2
disk1
disk1s1
```

上面的例子中，`disk1s1` 就是我们的 USB 设备。

<details>
<summary>但我这里什么都没有多出来啊？</summary>

我没试过，不过可以尝试下网络上提到的方法。一条条输入下面的命令，直到出现为止：

```bash
launchctl load /System/Library/LaunchDaemon/com.apple.disk*
launchctl load /System/Library/LaunchDaemon/com.apple.kextd.plist
launchctl load /System/Library/LaunchDaemon/com.apple.notifyd.plist
launchctl load /System/Library/LaunchDaemon/com.apple.configd.plist
launchctl load /System/Library/LaunchDaemon/com.apple.DirectoryServices.plist
```

</details>

## 装载 USB 设备

接下来我们确认 USB 设备类型。如果按上面的例子 `disk1s1`，我们输入：

```bash
fstyp /dev/disk1s1
```

我这里输出的是:

```
msdos
```

你可能会不一样，不过没有关系，先启用读写模式然后创建临时文件夹。输入：

```
mount -uw/
mkdir /az
```

接着把 USB 设备装载到 `az` 这个临时文件夹里。如果按上面例子的 `disk1s1` 和 `msdos`，输入

```
mount -t msdos /dev/disk1s1 /az
```

## 复制文件夹

{% note warning %}

注意如果文件夹名字里面有空格，要在空格前面加一个反斜杠（\）

{% endnote %}


输入 `cp -pr 源文件夹 /az/` 就可以把它拷贝到 USB 设备上了。举个例子，我们把桌面复制过来：

```bash
cp -pr /Users/你的用户名/Desktop /az/
```

如果你不知道文件在什么地方的话，输入 `ls` 会显示当前目录下所有的文件和文件夹，`cd 文件夹名` 可以进入那个文件夹，`cd ..` 可以返回上级文件夹。你还可以试着按 `tab` 键，它可能会帮你自动补全文件的名称。

{% note success %}

要创建 zip 压缩包的话通过输入 `zip -rX 文件名.zip 要压缩的文件夹`

{% endnote %}

## 收工

推出磁盘并关机。输入：

```bash
umount /az/
shutdown -r now
```

最后祝您身体健康。
