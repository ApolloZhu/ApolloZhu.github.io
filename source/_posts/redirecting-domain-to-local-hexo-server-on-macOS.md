---
title: macOS 重定向域名到 hexo 本地服务器
date: 2017-03-18 16:36:34
tags:
- macOS
- tips
- server
- hexo
categories:
- 瞎捣鼓
---

每次把网站截屏发朋友圈，被别人发现地址栏是 `localhost:4000`，稍微觉得有点 low。也是，怎么也得展示个像样点的域名吧。所以在网上查了查，整理收集如下。我对网络基本不了解，望各位路过的大神们指点一二。

<!-- more -->

## 修改 hosts

假设我们很有逼格的域名是 `example.com`

通过 `/etc/hosts` 把 `example.com` 映射到 `10.0.0.1`

```sh
10.0.0.1 example.com
```

## 配置

一下步骤每次**重启都要再执行一遍**

在回环接口（loopback interface）新建一个地址，`10.0.0.1`

```sh
sudo ifconfig lo0 alias 10.0.0.1
```

`-e` 启动防火墙（Packet Filter），`-f` 载入后面的规则 —— 将所有到 `10.0.0.1:80`（HTTP 默认端口）的连接转发到 `127.0.0.1:4000`（hexo 默认本地服务器地址）

```sh
echo "rdr pass on lo0 inet proto tcp from any to 10.0.0.1 port 80 -> 127.0.0.1 port 4000" | sudo pfctl -ef -
```

完成，现在可以在浏览器中输入 `example.com` 来代替了！

----

## 还原

重启电脑，或是

删除新建的地址，重置防火墙，清空本地 DNS 缓存

```sh
sudo ifconfig lo0 -alias 10.0.0.1
sudo pfctl -F all -f /etc/pf.conf
dscacheutil -flushcache
```

----

## 参考

1. [iptables equivalent for mac os x - StackExchange](https://serverfault.com/questions/102416/iptables-equivalent-for-mac-os-x/)
