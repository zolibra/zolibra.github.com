---
layout: post
title: "[leetcode]Palindrome Number "
description: ""
category: 
tags: [leetcode]
---
{% include JB/setup %}
Determine whether an integer is a palindrome. Do this without extra space.

123454321 is a Palindrome Number while -123454321 is not，注意stack overflow问题

可以Reuse Reverse Integer的code:

	package leetcode;
	
	public class PalindromeNumber {
	    public int reverse(int x){
	        if(x < 0)return 0;
	        boolean isNagtive = false;
	        if (x<0){
	            isNagtive = true;
	            x = -x;
	        }
	        long y = 0;
	        while (x/10 > 0){
	            y = y*10 + x%10;
	            x /= 10;
	        }
	        y = y*10 + x;
	        if (y>0x7fffffff) return 0; //overflow check.
	        if(isNagtive)y = -y;
	        return (int)y;
	    }
	
	    public boolean isPalindrome(int x) {
	        if(reverse(x) == x)return true;
	        return false;
	    }
	}
	
思考，用递归怎么解决？