---
title: 连我都不会的自然语言处理
tags:
  - linguistics
categories:
  - 生活
date: 2020-04-14 16:42:06
---

> The trophy would not fit in the brown suitcase because **it** was too big.

<!-- more -->

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

在华大的时候，周五晚上我一般会和同学聚一聚，而不知道为什么有天晚上就聊到了这句话。按语法来说这应该属于指代不明，但人可以通过生活经验判断出这里的 `it` 指代的是奖杯（这奖杯还挺大）。可能上面这个对机器来说是个[挑战](https://cmte.ieee.org/futuredirections/2014/08/20/whats-too-big-the-trophy-or-the-suitcase/)，那下面这些例子可能连我们都需要想一想才能理解。

## 排除错误断句

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">A Wild Charging Case with Both <a href="https://twitter.com/hashtag/AirPods">#AirPods</a> Appeared!</p>&mdash; Zhiyu (Apollo) Zhu (@zhuzhiyu_) <a href="https://twitter.com/zhuzhiyu_/status/1243167617482924035">March 26, 2020</a></blockquote>

对于上面这条推文，你可以理解为一个被过度修饰的名词短语：

```Lisp
((wild) charging case (with (both) AirPods appeared))
```

但我们需要将这个可能性排除：

<blockquote class="twitter-tweet"><p lang="zh" dir="ltr">你这里 with + sth + p.p. 是过去分词作伴随状语，可是你看看 appear 和 AirPods 的关系是被动的吗？更何况 appear 是一个不及物动词</p>&mdash; <strong>Captain 雪ノ下八幡</strong> (@HachimanCaptain) <a href="https://twitter.com/HachimanCaptain/status/1243169509831143424">2020/03/26</a></blockquote>

而改为理解成一个完整的句子：

```Lisp
((wild) charging case (with (both) AirPods) appeared)
```

和“我一把把把把住了”一样，我们能够在简单的试错之后成功断句。不过接下来可不仅仅是脑经急转弯，而是真的烧脑了。

## 运用逻辑思维进行语义分析

针对下面这个要求，需要列出我刚好四个月前那一天去过的商店吗？请在不展开看同义改写的情况下思考：

<pre><code><details><summary>List all shops that you have not visited since more than 4 months ago.</summary>  List all shops that you          visited    earlier than 4 months ago.
  List all shops that you have not visited   for more than 4 months.
  List all shops that you have not visited within the last 4 months.</details></code></pre>

我不知道你是否一下子就理解了这个句子，但我个人认为任何一个改写都比原句更容易理解，而且能够更迅速地帮你分析出上面那个问题的答案。那理解这个句子究竟难在哪里呢？个人推测有以下几个原因：

1. since 后面一般会是一个固定的时间点，但 more than 是一个时间段（for 尝试解决的问题）
2. more than 一般是正向的，但我们在讨论逆向的 ago（earlier 尝试解决的问题）
3. not ... since 和 not ... more than 两种组合的可能性，以及两者逻辑上处理的不同
    1. not ... since，就像改写一里那样，可以被直接去掉
    2. not ... more than 按照逻辑则是改为 ≤

虽然可能 Spring 2020 上 CSE 414 的人里只有我（因为被扣了一分）在纠结这个问题，但（过去、现在、将来）看到这个句子一头雾水的绝对不止我一个：

{% blockquote Rebecca Taylor, ENGL 131 instructor @UW %}
In all honesty, the sentence was a brain-bender — we had to read it aloud several times because the wording was confusing. I can easily see how it could be interpreted differently.
{% endblockquote %}

---

我们经常谈论 accessibility，那么我认为让所有人都能够看懂题也是非常重要的一部分。UW 的 INFO 200 在这方面我认为就处理得特别好，甚至还在写作、阅读方面照顾英语不是那么好的同学。在华大不少 competitive major 都想方设法让学生丢分的潮流中，祝 iSchool 能够继续坚守以学术--而不是竞争--为目标，展示（计算机）教育的本质。


<a href="https://computinged.wordpress.com/2020/07/27/proposal-2-to-change-cs-education-to-reduce-inequity-stop-allocating-rationing-or-curving-down-grades" target="_blank" style="position:relative;text-decoration:none;display:-webkit-box;display:-ms-flexbox;display:flex;-webkit-box-pack:justify;-ms-flex-pack:justify;justify-content:space-between;margin-top:16px;margin-bottom:16px;cursor:pointer;border:1px solid #e7eaf1;border-radius:4px;box-shadow: 0 1px 3px 0 rgba(0,34,77,.05);">
  <img src="https://secure.gravatar.com/blavatar/cdf22afe2630f1473c2def7289f11fee?s=200" style="border:none;padding:0;-ms-flex-negative:0;flex-shrink:0;width:90px;height:90px;-o-object-fit:cover;object-fit:cover;margin-bottom:0;border-radius:3px;">
  <span style="display:-webkit-box;display:-ms-flexbox;display:flex;width:100%;padding:10px 16px;overflow:hidden;-webkit-box-orient:vertical;-webkit-box-direction:normal;-ms-flex-direction:column;flex-direction:column;-ms-flex-pack:distribute;justify-content:space-around;">
    <span style="font-size:18px;font-weight:400;text-overflow:ellipsis;overflow:hidden;word-wrap:normal;white-space:nowrap;">Proposal #2: Make the highest grades achievable by all</span>
    <span style="overflow:hidden;font-size:15px;color:#8798ae;text-overflow:ellipsis;word-wrap:normal;white-space:nowrap;">To Change CS Education to Reduce Inequity 
      <span style="display:inline-block;padding:1px 6px;margin-left:8px;font-size:12px;line-height:normal;color:#8590a6;vertical-align:1px;background-color:#f7f8fa;border-radius:3px;">Computing Education Research Blog</span>
    </span>
  </span>
</a>
