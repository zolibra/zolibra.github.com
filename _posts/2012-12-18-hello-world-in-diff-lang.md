---
layout: post
title: "简单就是好“
description: ""
category: 
tags: [python,lisp,c,java]
---
{% include JB/setup %}

随着编程语言的发展，越来越多的语言追求简单的句法，庞大的库，最近比较了一下，语言的发展似乎又回到了原始的50年代，tmd再次鄙视某些语言一百遍。
以Hello world为例做一个简单的比较

优雅的Lisp语言发明于上世纪50年代：
------

   ('Hello world)
	
Unix shell出生于上世纪60年代的bell labs
------

	#!/bin/bash
	echo "Hello World"
	
	
C语言70年代诞生，同样出自bell labs...
------

    void main(){
		printf("Hello World")
	}

JAVA......
------

    Class HelloWorld
	{
		public static void main(String args[])
			{
				System.out.println("Hello World")
			}
	}
	
Python
------

	print ”Hello World"
	
Ruby
-----

	puts "Hello World"
	
	
看出趋势来没？语言在发展了半个世纪之后越来越趋向于Lisp语言
	
	
