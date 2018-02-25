---
title: 制作 Telegram 表情包
date: 2018-02-25 08:40:01
keywords:
- telegram
- 表情包
- photoshop
tags:
- tips
categories:
- 瞎捣鼓
---

在制作 [百地 たまて](http://slow-start.com/#tamate) 的[表情包](https://t.me/addstickers/TamateMomochi)的时候，才知道 telegram 和微信一样对表情包有要求，512 px 加白边。纵使别人连 psd 文件都给你们了，你们还是照样不遵守规范……所以让我们来看看选中 Layer 后要加些啥 ***fx***：

{% fi https://user-images.githubusercontent.com/10842684/36642537-a9badbe4-1a0e-11e8-99f4-200281c3ad24.png %}

<!-- more -->

## Outer Glow

### Stucture
Blend Mode: Screen
Opacity: 100%
Noise: 0%
Color: #fcfcfc

### Elements
Technique: Softer
Spread: 89%
Size: 5px

### Quality

Contour: Linear
Anti-aliased: 自行判断
Range: 50%
Jitter: 0%

## Drop Shadow

Layer knocks Out Drop Shadow: YES

### Stucture

Blend Mode: Multiply
Color: #000000
Opacity: 25%
Angle: 120
Use Global Light: YES
Distance: 5px
Spread: 0%
Size: 10px

### Quality

Contour: Linear
Anti-aliased: 自行判断
Noise: 0%

{% fi https://user-images.githubusercontent.com/10842684/36642777-3d1d27e0-1a12-11e8-88e1-77aa003d887f.png %}

你学会了吗？
