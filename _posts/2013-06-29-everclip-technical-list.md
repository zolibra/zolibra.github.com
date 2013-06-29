---
layout: post
title: "EverClip技术列表"
description: ""
category: 
tags: [IOS,Evernote,EverClip]
---
{% include JB/setup %}

Everclip是一款可以在IOS设备上copy paste 内容，并且同步到Evernote 的应用，由[@siuying](https://twitter.com/siuying) 的三人团队完成，获得了2012年Evernote 的 DevCup大奖，Everclip实验了RubyMotion快速开发IOS应用的先河，使用到的很多IOS开源技术值得借鉴，本文对其使用的技术作简短介绍。 

**AFNetworking**

IOS平台非常流行的网络框架，2012iOS Library奖.AFNetworking包括了所有你需要与在线资源交互的内容，从web services到文件下载。

**CocoaLumberjack**

与log4j类似的logging Framework，据说比NSLog还要快
<https://github.com/robbiehanson/CocoaLumberjack>

**cocosDenshion**

用来播放背景声音和音效,some examples:
<https://github.com/ndubbs/CocosDenshion-Example>

**DCRoundSwitch**

UISwith的一个替代品，可以custome 他的apperance

**DTWebArchive**

用来解析 UIPasteboard 的WebArchive内容
<https://github.com/Cocoanetics/DTWebArchive>

**Evernote-SDK-iOS**

这个不用说了，Evernote的官方IOS SDK

**JSTokenField**

这个应该是用来实现note的Tag 的 Token效果
<https://github.com/jasarien/JSTokenField>

**LRTableModel**

haha,看看它在github上的title：
_LRTableModel, because implementing UITableViewDataSource sucks!_
一个UITableViewDataSource的替代品
<https://github.com/lukeredpath/LRTableModel>

**MBProgressHUB**

这个大家都熟悉了,最流行的等待指示器
<https://github.com/jdg/MBProgressHUD>

**NSData+MD5Digest**

加入了MD的NSData category
<https://github.com/siuying/NSData-MD5>

**NYXImagesKit**

NYXImagesKit 包含一组很有用的 UIImage 图像处理方法，包括 filtering, blurring, enhancing, masking, reflecting, resizing, rotating, saving. 同时也提供了一个 UIImageView 的之类，支持异步的从 URL 下载图像并显示。
<https://github.com/Nyx0uf/NYXImagesKit>

**NanoStore**

NanoStore是一个轻量开源的基于Key Value的文档数据库
<https://github.com/tciuro/NanoStore>

**PSTCollectionView**

又一个替代品，替代UICollectionView，用来支持多版本。
If you want to have PSTCollectionView on iOS4.3/5.x and UICollectionView on iOS6, use PSUICollectionView
<https://github.com/steipete/PSTCollectionView>

**QuickDialog**

QuickDialog可以快速创建Form，而不用再跟UITableView，delegate，and DataSource打交道
<https://github.com/escoz/QuickDialog>

**Reachability**

一个Apples 官方 Reachability API的替代品，用以探测网络环境
<https://github.com/tonymillion/Reachability>

**UIGlossyButton**

不用图片创建类似iOS默认样式的按钮
<https://github.com/waterlou/UIGlossyButton>

**WebContentView**

处理Rich HTML like What UIWebView Does, 他不会load URLs，可以把它看作是一个Rich版本的UIWebView
<https://github.com/nicklockwood/WebContentView>

**YIPopupTextView**

类似Facebook的发post的kit，Everclip用它来创建新note
<https://github.com/inamiy/YIPopupTextView>

**hpple**

HTML／XML 解析器
<https://github.com/topfunky/hpple>

**iPhoneMK**

一个工具集，Views，TableViewCells…哎，为什么大家都不爱用apple原生的呢？
<https://github.com/michaelkamprath/iPhoneMK>

**SimpleView**

RubyMotion DSL for UIKit
<https://github.com/seanho/SimpleView>


