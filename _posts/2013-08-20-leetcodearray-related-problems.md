---
layout: post
title: "[leetcode]数组问题Reverse string & Evaluate Reverse Polish Notation"
description: ""
category: 
tags: [java, algorithsm, array]
---
{% include JB/setup %}

###Problem 1：Reverse string word by word
Given an input string, reverse the string word by word.

For example,

	Given s = "the sky is blue",
	return "blue is sky the".

Clarification:
What constitutes a word?
A sequence of non-space characters constitutes a word.
Could the input string contain leading or trailing spaces?
Yes. However, your reversed string should not contain leading or trailing spaces.
How about multiple spaces between two words?
Reduce them to a single space in the reversed string.

**Solution1:**

    private static String revertString1(String s){
        if (s == null){
            return "";
        }
        s.trim();
        if (s == null){
            return "";
        }

        if (s == ""){
            return "";
        }

        StringBuffer newStr = new StringBuffer();
        String s2 = s.replaceAll(" +" ," ");
        String[] newArray = s2.split(" ");
        for (int i = newArray.length -1 ; i >= 0 ;i--){
            newStr.append(newArray[i]);
            newStr.append(" ");
        }

        return newStr.toString().trim();
    }

也可以替换以下代码, 注意：*Split接受的是正则表达式*

    String s2 = s.replaceAll(" +" ," ");
    String[] newArray = s2.split(" ");
    
为：

	String[] newArray = s.split("\\s+");

不知道大Inter们会不会challenge用正则。

###Problems 2: Evaluate Reverse Polish Notation

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

Some examples:
	
	["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
    ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6
    
**Solution1:** 利用堆栈

    private static int evalRPN(String[] tokens) {
        if (tokens == null | tokens.length == 0){
            return 0;
        }
        Stack<Integer> stack= new Stack<Integer>();
        for (int i = 0; i < tokens.length; i++) {
            if (!isOperator(tokens[i])){
                stack.add(Integer.parseInt(tokens[i]));
            }else {
                if (stack.size() < 2)continue;
                int a = stack.pop();
                int b = stack.pop();
                if (tokens[i].equalsIgnoreCase("+")){
                    stack.add(b + a);
                }else if (tokens[i].equalsIgnoreCase("-")){
                    stack.add(b - a);
                }else if (tokens[i].equalsIgnoreCase("*")){
                    stack.add(b * a);
                }else if (tokens[i].equalsIgnoreCase("/")){
                    if (b == 0 || a == 0){
                        stack.add(0);
                        continue;
                    }
                    stack.add(b / a);
                }
            }
        }
        return stack.pop();
    }
    
注意pop出来的两组数的操作顺序。
