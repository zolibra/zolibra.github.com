---
layout: post
title: "Markdown Syntax"
description: ""
category: 
tags: [markdown, jekyll]
---
{% include JB/setup %}

#标题
This is an H1
=============
This is an H2
-------------

#Blockquotes

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

#列表

*   Red
*   Green
*   Blue

#代码
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
    

Use the `printf()` function.

#链接
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

[Google]: http://google.com/

#强调
*single asterisks*

_single underscores_

**double asterisks**

__double underscores__


