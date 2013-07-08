---
layout: post
title: "Play Python With Sublime2"
description: ""
category: 
tags: [python,Sublime,pdb]
---
{% include JB/setup %}

最近Sublime编辑器很流行，于是也上手玩玩，尝试用它整合python 的IDE环境，觉得还不错，利用sublime方便的package管理机制，很快的搭建起来。

首先打开Sublime 2, Command＋shift＋P --> 'ip' 依次安装python的IDE环境需要以下插件：

Package Name |     Usage      
------------ | ---------------
SublimeRope  | Autocompletion, Go to Definition
SideBarEnhancemnt| Enhance some feature in the side bar
SublimeLinter| Code Check
SublimeREPL | Debug using PDB

如何用SublimeREPL Debug Python：

in case I have below example code：

    def test(str):
         print str

    if __name__ == '__main__':
         print 'start main'
         print 'ready to record test'
         l = test('test')
         print 'after record test'
         
In Sublime , Tool-->SublimeREPL-->Python-->PDB current file
一些Debug有用的命令：

命令	      | 解释
--------- |  ----
break 或 b |设置断点	设置断点
continue 或 c|	继续执行程序
list 或 l	|查看当前行的代码段
step 或 s	|进入函数
return 或 r	|执行代码直到从当前函数返回
exit 或 q	|中止并退出
next 或 n	|执行下一行
pp	|打印变量的值

Below are some output when i type 'n' on the example code:

    > /Users/chengray/mywork/Python/test/test.py(1)<module>()
    -> def test(str):
	(Pdb) n

	> /Users/chengray/mywork/Python/test/test.py(4)<module>()
	-> if __name__ == '__main__':
	(Pdb) > /Users/chengray/mywork/Python/test/test.py(5)<module>()
	-> print 'start main'
	(Pdb) n

	start main
	> /Users/chengray/mywork/Python/test/test.py(6)<module>()
	-> print 'ready to record test'
	(Pdb) ready to record test
	> /Users/chengray/mywork/Python/test/test.py(7)<module>()
	-> l = test('test')
	(Pdb) n

	test
	> /Users/chengray/mywork/Python/test/test.py(8)<module>()
	-> print 'after record test'
	(Pdb) after record test
	--Return--
	> /Users/chengray/mywork/Python/test/test.py(8)<module>()->None
	-> print 'after record test'
	(Pdb) 
	
Resources:
<http://outofmemoryblog.blogspot.sg/2012/08/python-development-with-sublime-text-2.html>