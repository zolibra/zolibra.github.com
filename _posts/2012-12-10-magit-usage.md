---
layout: post
title: "Magit替代Git bash "
description: ""
category: 
tags: [Git,Emacs,Magit]
---
{% include JB/setup %}

  首先最好先重新定义一下window的HOME环境变量，设置为'.gitconfig'所在的dir，否则Magit使用中会因为找不到git bash的config文件出现一些问题，比如autocrcf，username，email等配置。再比如，push失败等。
下边介绍一些常用的magit 命令

Status:
----
    M-x magit-status 

Stage:
----
    M-x magit-status 
	s to stage file
Commit：
----
    M-x magit-status
	'c' to commit file , and type the commit message
	C-c C-c
	
Push:
----
    M-x magit-status
	P P

Pull:
----
    M-x magit-status
	F F

	
