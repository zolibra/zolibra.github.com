---
layout: post
title: "[leetcode]String to Integer"
description: ""
category: 
tags: [leetcode, String]
---
{% include JB/setup %}

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

容易忽略的case， +123, overflow

	public class atoi {
	
	    public int charToNum(char c){
	        int num = c - '0';
	        if(num >= 0 && num <= 9)return num;
	        return 0;
	    }
	
	    public int atoi(String s) {
	        s = s.trim();
	        long ans = 0L;
	        boolean isNegative = false;
	        if (s.length() == 0) return 0;
	        if (s.length() == 1) return charToNum(s.charAt(0));
	        if (s.charAt(0) == '-') isNegative = true;
	        int pos = 0;
	        if (isNegative||s.charAt(0) == '+')pos++;
	
	        while ((pos < s.length()) && s.charAt(pos) >= '0' && s.charAt(pos) <= '9') {
	            ans = ans * 10 + (s.charAt(pos) - '0');
	            pos++;
	            //Negative
	            if (ans > 0x7fffffff) return isNegative ? Integer.MIN_VALUE : Integer.MAX_VALUE;//overflow check
	        }
	        return isNegative ? -(int) ans : (int) ans;
	    }
	
	    public static void main(String[] args) {
	        atoi a = new atoi();
	        String[] arr = {"   -123", "12 3", "abcd", "-", "12321234123412431243124","   010"};
	        for (int i = 0; i < arr.length; i++) {
	            System.out.println(a.atoi(arr[i]));
	        }
	    }
	}

leetcode solution还是比较clean的，有几点值得借鉴

1. overflow check可以用MAX/10来比较，省的定义输入为long，还要强转
2. 正负可以用一个sign，省去了return用表达式


Code:

	private static final int maxDiv10 = Integer.MAX_VALUE / 10;
	
	public int atoi(String str) {
	   int n = str.length();
	   int i = 0;
	   while (i < n && Character.isWhitespace(str.charAt(i))) i++;
	   int sign = 1;
	   if (i < n && str.charAt(i) == '+') {
	      i++;
	   } else if (i < n && str.charAt(i) == '-') {
	      sign = -1;
	      i++;
	   }
	   int num = 0;
	   while (i < n && Character.isDigit(str.charAt(i))) {
	      int digit = Character.getNumericValue(str.charAt(i));
	      if (num > maxDiv10 || num == maxDiv10 && digit >= 8) {
	         return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
	      }
	      num = num * 10 + digit;
	      i++;
	   }  
	   return sign * num;
	}
	
	
