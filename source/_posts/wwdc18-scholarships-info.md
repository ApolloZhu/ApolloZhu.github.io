---
title: WWDC18 Scholarships Information
date: 2018-03-15 19:42:39
keywords:
tags:
- Swift
- WWDC18
- WWDC
- English
categories:
- 编程
---

<details>
<summary>Wait, before we start, what is WWDC?</summary>

I'll add my description soon, but for now, check out the [official website](https://developer.apple.com/wwdc).
</details>

Thank you all for being interested in [Apple's Worldwide Developer Conference](https://developer.apple.com/wwdc) and [this scholarship opportunity](https://developer.apple.com/wwdc/scholarships/). I hope all of us could go together, to learn, and have fun!

I know this article is a little bit long, but please read through this carefully before you start. If you have any questions, just ask me through messenger, or in the comment area below.

> I'll be constantly updating this, and the Chinese version is available [here](https://apollozhu.github.io/2018/03/16/wwdc18-scholarships-info-cn/).

<!-- more -->

## Important Dates

|Date|Event|
|--:|--|
|April 1, 20:00 EDT|Submission Due|
|April 20|Announce Status|
|June 3-8|Orientation + WWDC!|

## General Information

Please read the [description](https://developer.apple.com/wwdc/scholarships/) carefully, as well as the [terms and conditions](https://developer.apple.com/wwdc/scholarships/terms/WWDC18-Scholarship-Terms-and-Conditions.pdf). In summary, you are required to write a Playground -- an interactive program -- that is creative and technically accomplished.

## Things to Get

You do ***NOT*** need a paid Apple Developer Account. Do you know what's better than that? You'll get one year of Apple Developer membership if you win!

If you have a Mac, download [Xcode from Mac App Store](https://itunes.apple.com/app/id497799835), or if you have an iPad, download [Swift Playgrounds from App Store](https://itunes.apple.com/app/id908519492), or if you have a Windows, get a virtual machine or whatever that works.

## Learn Swift

If you have an iPad, I highly recommend you to go through one of those "Learn to Code" playgrounds to get a general idea about what a legit playground should be like, in addition to the Swift programming language itself.

At the same time, everyone by now should have either an iOS device or a Mac, please open (i)Books and get *[The Swift Programming Language](https://itunes.apple.com/book/id1002622538)*. You can always choose to [read it online](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/index.html) as well.

Most of you are already familiar with Java, so reading just "A Swift Tour" should be adequate for you to understand this simple programming language. For those of you never learned programming before, just scan through that, and chapter 2 (Language Guide) will answer your questions.

You do *NOT* need to read chapter 3 (Language Reference) and 4 (Revision History).

## General Stuff to Learn

### I Want to Write a 2D game

You should learn [SpriteKit](https://developer.apple.com/spritekit/).

### I Want to Write a 3D game

You should learn [SceneKit](https://developer.apple.com/scenekit/), but I hope you've already had some sense of how 3D works and where to get your 3D models. A bonus for you, [Apple talked about using SceneKit in the iPad version of Swift Playgrounds](https://developer.apple.com/videos/play/wwdc2017/605/).

### Otherwise

Well, [UIKit](https://developer.apple.com/documentation/uikit) itself can do a lot of stuff. To get started, follow [Start Developing iOS Apps (Swift)](https://developer.apple.com/library/content/referencelibrary/GettingStarted/DevelopiOSAppsSwift/).

If you have time, you may also want to have a general understanding of how [view controllers work](https://developer.apple.com/library/content/featuredarticles/ViewControllerPGforiPhoneOS), maybe more about [table views](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/TableView_iPhone/AboutTableViewsiPhone/AboutTableViewsiPhone.html), or even [iOS Apps in general](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html).

## More About Playground

No matter what, you should read the [Markup Formatting Reference](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_markup_formatting_ref/). Your Playground will look a lot better with this in conjunction with `CustomPlaygroundQuickLookable`/`CustomPlaygroundDisplayConvertible`.

### Mac, Xcode, and Playground

It was first [introduced back in 2014](https://developer.apple.com/videos/play/wwdc2014/408/), and later in 2015 you can use the format mentioned above to [author rich Playgrounds](https://developer.apple.com/videos/play/wwdc2015/405/) to better instruct your users. Here is [a simple Swift Playground Book](https://developer.apple.com/library/content/samplecode/StarterPlaygroundBook/Introduction/Intro.html) for you to get started, and you can also find other interesting ones from the [Swift Blog](https://developer.apple.com/swift/blog/), although many of them would be outdated and require some changes for them to work.

### iPad and Swift Playgrounds

This app is first [introduced in 2016](https://developer.apple.com/videos/play/wwdc2016/408/) and [updated again last year](https://developer.apple.com/videos/play/wwdc2017/408/). iPad Playground has many features that a normal Xcode Playground doesn't have -- Cut Scenes written in html (a great place to inform your user what's this chapter about), cover images, vocab lists, etc. To fully utilize those features, please read the [Playground Book Format Reference](https://developer.apple.com/library/content/documentation/Xcode/Conceptual/swift_playgrounds_doc_format/), and experiment with [this sample](https://developer.apple.com/library/content/samplecode/TalkingToTheLiveView/Introduction/Intro.html) that allows you to send messages to a Swift Playground live view and saving data to its key-value store.

## Analysis

Remember that your playground will be judged offline, the program can ***NOT*** require an account for sign in, and they'll only spend 3 minutes in judging it, so think about what you are going to do. Even without thinking I can tell you many people will be doing [augmented reality](https://developer.apple.com/arkit) and [machine learning](https://developer.apple.com/coreml); you can not imagine how easy it is to implement those fancy but scary stuff with ARKit and Core ML. Well, try to be creative, add some graphics and audios, and incorporate some of Apple's new technologies (even if they didn't mention about that)…

For the first time, you are allowed to use open source frameworks (providing that you included their licenses correctly and explained why). Nonetheless, what you are going to submit is not just a normal program. I think these are some reasons why Apple prefers Playground over normal apps, and maybe you want to address some of them:

1. user will be directed about what to do and informed of what is expected
2. it provide an interactive way for the users to [learn things through programming](https://developer.apple.com/videos/play/wwdc2017/416/)
3. it sparks users' interest in coding and encourages further participation
4. ...(many more to add)

Also, the "Beyond WWDC" essay is very important. You should explain, in 500 words, how you share your coding knowledge and enthusiasm for computer science with others. Spend some time on this and revise it several times.

However, that doesn't mean the playground itself isn't important. There were many amazing playgrounds, such as [this one here](https://www.youtube.com/watch?v=cq_zLMKB-SE), but the quality of the [other ones](https://www.youtube.com/playlist?list=PLl469UE7Uwr0bdon2CvnpxmQs16qu4nkf) varies. So my suggestion is analysis why some of them got accepted and some got rejected, see if you can resonate with [former winners](https://itunes.apple.com/story/id1358780266), and just try your best.

If you'd ever ask me if it's hard, I'll answer yes but ***DOABLE***. Just make sure you don't copy any others' code -- the [2048 playground](https://github.com/wwdc/2017/issues/7) from [last year's submissions](https://github.com/wwdc/2017) was **rejected** for this reason.

{% centerquote %}
Everything is doable if you try.

**Mr. Lau**
{% endcenterquote %}

Good luck.

-- Apollo (a.k.a Zhiyu Zhu, last year's scholarship winner for submitting [Karel the Robot Playground](https://github.com/ApolloZhu/Swifty-Karel/tree/master))
