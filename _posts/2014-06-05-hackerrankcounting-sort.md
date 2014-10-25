---
layout: post
title: "[hackerrank]Counting Sort"
description: ""
category: "算法"
tags: [hackerrank, java, sort]
---
{% include JB/setup %}
计数排序

**Input Format 
**

n - the size of the list ar. 
n lines follow, each containing an integer x, and a string, s.

**Output Format **

Print the strings in their correct order.

**Constraints** 

1 <= n <= 1000000 
n is even 
1 <= length(s) <= 10 
0 <= x < 100 , x ∈ ar 
The characters in every string s is in lowercase.

**Sample Input
**

	20
	0 ab
	6 cd
	0 ef
	6 gh
	4 ij
	0 ab
	6 cd
	0 ef
	6 gh
	0 ij
	4 that
	3 be
	0 to
	1 be
	5 question
	1 or
	2 not
	4 is
	2 to
	4 the
	
**Sample Output
**

	- - - - - to be or not to be - that is the question - - - -
	
**Implementation:
**

	import java.io.*;
	import java.util.*;
	import java.text.*;
	import java.math.*;
	import java.util.regex.*;
	
	public class Solution {
	    public static void main(String[] args) throws Exception {
	        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
	        int n = Integer.parseInt(in.readLine());
	        StringBuffer[] array = new StringBuffer[100];
	        for(int i = 0; i < 100; i++) {
	            array[i] = new StringBuffer();
	        }
	        for(int i = 0; i < n; i++) {
	            String[] line = in.readLine().split(" ");
	            int v = Integer.parseInt(line[0]);
	            String s = line[1];
	            array[v].append(i < n / 2 ? "-" : s).append(" ");
	        }
	        for(int i = 0; i < 100; i++) {
	            System.out.print(array[i]);
	        }
	        System.out.println();
	    }
	}
	
计数排序：
算法符合特点： 整数有限范围 如 1~100 ，输入表长度为N
要点： count 数组 ，helper 数组(需要访问原始数组的情况)