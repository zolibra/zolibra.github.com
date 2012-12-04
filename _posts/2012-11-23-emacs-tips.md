---
layout: post
title: "Emacs tips"
description: ""
category: 
tags: []
---
{% include JB/setup %}

* 配置文件位置：
          options-save options 
D:\Documents and Settings\hchen018\Application Data\.emacs


* 小结（SUMMARY）
-----------------
 
翻页浏览时相当有用：
 
         C-v     向前移动一屏
         M-v     向后移动一屏
         C-l     重绘屏幕，并将光标所在行置于屏幕的中央
                 （注意是 CONTROL-L，不是 CONTROL-1）
                   
* 基本的光标控制（BASIC CURSOR CONTROL）
----------------------------------------
 
 
                              上一行 C-p
                                   :
                                   :
             向左移 C-b .... 目前光标位置 .... 向右移 C-f
                                   :
                                   :
                              下一行 C-n
                                    
                                    
         C-f     向右移动一个字符
         C-b     向左移动一个字符
 
         M-f     向右移动一个词【对中文是移动到下一个标点符号】
         M-b     向左移动一个词【对中文是移动到上一个标点符号】
 
         C-n     移动到下一行
         C-p     移动到上一行
 
         C-a     移动到行首
         C-e     移动到行尾
 
         M-a     移动到句首
         M-e     移动到句尾
                                  
         M-<(shift)     移动到文章最开始
         M->(shift)     移动到文章结尾
         
* 在 EMACS 失去响应的时候（WHEN EMACS IS HUNG）
-----------------
         C-g 终止命令
         
* 窗格（WINDOWS）
-----------------
         C-x 1   只保留一个窗格（也就是关掉其它所有窗格）
         
* 插入与删除（INSERTING AND DELETING）
-----------------

         <Delback>    删除光标前的一个字符
         C-d          删除光标后的一个字符
 
         M-<Delback>  移除光标前的一个词
         M-d          移除光标后的一个词
 
         C-k          移除从光标到“行尾”间的字符
         M-k          移除从光标到“句尾”间的字符
         C-@ 移动 C-w 移除选定的一部分缓冲区
	 C-u 8 *      这将会插入 ********
* 撤销（UNDO）
-----------------
         C-x u     撤销

* 文件（FILE）
-----------------
         C-x C-f   寻找一个文件
         C-x C-s   储存这个文件
	 C-x C-f Return 用d标记一个文件为D，用x操作统一删除

* 缓冲区（BUFFER）
----------------- 
         C-x C-b   列出缓冲区
         C-x b foo   以回到文件“foo”的缓冲区

* 搜索（SEARCHING)
-----------------
 
         C-s      是向前搜索
         C-r      是向后搜索

 【你会发现 C-g 会让光标回到搜索开始的位置，而 <Return> 则让光标留在搜索结果上，这是很有用的功能。】 

* 多窗格（MULTIPLE WINDOWS） 
-----------------
         C-x 2     分成两个创个
         C-M-v    滚动下方的窗格    
         C-x o     将光标移动到下方窗格
* 宏 (Macro)
----------------

	 F3		开始录制宏
	 C-x C-k n	命名宏
	 F4  	 	停止录制宏
	 C-x e		执行宏

* 获得更多帮助（GETTING MORE HELP）   
-----------------
      
        最基本的帮助功能是 C-h c。输入 C-h c 之后再输入一个组合键，Emacs 会给出
这个命令的简要说明。      
