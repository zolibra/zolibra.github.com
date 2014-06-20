---
layout: post
title: "在sublime中编译运行java"
description: ""
category: "工具"
tags: [sublime, java]
---
{% include JB/setup %}

----
###第一步：设置 Java PATH 变量

这是第一步也是最基本的一步，用来设置编译和运行 Java 程序基本命令如 javac 和 java 的存放路径。

###第二步：创建批处理或者Shell脚本

**windows**

    [ -f "$1.class" ] && rm $1.class
    for file in $1.java
    do
    echo "Compiling $file........"
    javac $file
    done
    if [ -f "$1.class" ]
    then
    echo "-----------OUTPUT-----------"
    java $1
    else
    echo " "
    fi

**Linux**

    [ -f "$1.class" ] && rm $1.class
    for file in $1.java
    do
    echo "Compiling $file........"
    javac $file
    done
    if [ -f "$1.class" ]
    then
    echo "-----------OUTPUT-----------"
    java $1
    else
    echo " "
    fi

脚本文件移动到jdk的bin目录下

###第三步：修改 Javac.sublime-build

按照以下的步骤修改sublime text 2的编译系统脚本。
在选项卡Preferences > Browse Packages.. 打开sublime的包目录
转到Java Folder
打开 JavaC.sublime-build 替换下面的命令行
`"cmd": ["javac", "$file"],`
在 Windows 下使用以下命令替换
`"cmd": ["runJava.bat", "$file"],`
在 Ubuntu 下使用以下命令替换
`"cmd": ["runJava.sh", "$file_base_name"],`

###PS: 另外还有不需要runjava脚本的方法：

在Mac下配置 java 环境：

1. 在选项卡Preferences > Browse Packages.. 打开sublime的包目录
2. 转到Java Folder
3. 打开 JavaC.sublime-build 替换为下面的命令行

    {
        "cmd": ["sh", "-c", "javac $file_base_name.java && java $file_base_name"],
        "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
        "selector": "source.java"
    }


