---
title: yearglass／年轮项目
date: 2017-03-06 17:28:50
tags:
- Swift
- macOS
- CLI
categories:
- 瞎捣鼓
---

{% centerquote %}
愿能为君，暂留光阴
<div id="yearglass-web"></div>
{% endcenterquote %}

<script>
	const today = new Date();
	const year = today.getFullYear();
	const thisYear = new Date(year, 0, 1);
	const nextYear = new Date(year + 1, 0, 1);
	const oneDay = today.getMilliseconds();
	const passed = Math.floor((today - thisYear) / oneDay);
	const total = Math.floor((nextYear - thisYear) / oneDay);
	const percentage = passed / total;
	const space = 15;

	function repeat(s, n) {
		return new Array(Math.floor(n + 1)).join(s);
	}

	document.getElementById("yearglass-web").innerHTML = year + " 年已过去 " + Math.floor(percentage * 100) + "% [" + repeat("▇", space * percentage) + repeat("\\\\", space * (1 - percentage)) + "]";
</script>

For the English Version of this documentation, please visit: [yearglass](https://apollozhu.github.io/yearglass/)

<!-- more -->

在即刻／微博／推特上看到一个有趣的提醒，[year_progress](https://twitter.com/year_progress)，总的来说就是显示今年过去了的百分比。于是顺手就用 Swift 实现了一个终端的小程序：[年轮](https://github.com/ApolloZhu/yearglass)。发布的时候 2017 年才过去 17% 呢。

## 基本

### 下载

```sh
git clone https://github.com/ApolloZhu/yearglass.git
```

### 更新

```sh
cd yearglass;git pull;cd ..
```

### 卸载

卸载完成后还需手动删除配置，请参考下文。

```sh
rm -rf yearglass
```

## Terminal 配置

### 加入到终端启动列表

```sh
echo "swift ~/yearglass/main.swift" >> .bash_profile
```

### 注册 `yearglass` 命令

```sh
echo "alias yearglass='swift ~/yearglass/main.swift'" >> .bash_profile
```

### 删除配置

```sh
sed -i '' '/swift .*yearglass.main.swift/d' .bash_profile
```

## Oh My Zsh 配置

本人并不了解 zsh 怎么用，如有疏漏还请大家指正。

### 加入到终端启动列表

```sh
echo "swift ~/yearglass/main.swift" >> .zshrc
```

### 注册 `yearglass` 命令

```sh
echo "alias yearglass='swift ~/yearglass/main.swift'" >> .zshrc
```

### 删除配置

```sh
sed -i '' '/swift .*yearglass.main.swift/d' .zshrc
```
