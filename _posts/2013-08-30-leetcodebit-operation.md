---
layout: post
title: "[leetcode]位运算集合"
description: ""
category: 
tags: [leetcode, java, bit]
---
{% include JB/setup %}

###Problems 1: Single Number
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Solution 1:**
我的初始思路是:先快速排序，然后直接遍历，找到当前数组和下一位不同的返回：

    public static int singleNumber(int[] A) {

        quickSort(A, 0 , A.length - 1);

        for (int i = 0; i < A.length - 1; i++) {
            if (A[i] != A[i+1]){
                return A[i];
            }else{
                i++;
            }
        }
        return 0;

    }

Submit的时候被拒了，原因超时。。题目要求线性的runtime complexity。

**Solution 2:**采用位运算

    public static int singleNumber(int[] A, int n) {
        int result = 0;
        for (int i = 0; i < n; i++) {
            result ^= A[i];
        }
        return result;

    }

坑爹的利用了异或的(交换性)[http://longzxr.blog.sohu.com/190676432.html]
