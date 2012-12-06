---
layout: post
title: "Github显示中文编码"
description: ""
category: 
tags: []
---
{% include JB/setup %}

问题提出
----
由于Github后台是linux服务器，直接在本地用Mysisgit编辑的中文在Github上会出现乱码，一种方式是修改mysisgit配置，另一种方法是用其他编辑工具输出utf-8编码。
编辑工具可以选择emacs，或者notepad++也可以，notepad++里，菜单栏-->Encoding-->Convert utf-8 without BOM 即可。下边介绍一些emacs的key。

查看当前buffer的编码
----

    M-x describe-coding-system
	
列出所有编码
-----

    C-x <RET> r <TAB>
	
以指定编码重读当前buffer
-----

    C-x <RET> r utf-8，(revert-buffer-with-coding-system)

改变当前buffer编码
----

    C-x <RET> f uft-8， (set-buffer-file-coding-system)
	
设定下一步操作的编码格式
----

    C-x <RET> c ( M-x universal-coding-system-argument )
	




    


    
