---
layout: post
title: "[googlehack]Reverse words in string"
description: ""
category: 
tags: [googlehack, Array, leetcode]
---
{% include JB/setup %}

字符串翻转是经典面试题目，其有几种题型：

题型一： hello this is hui —> olleh siht si iuh，这种题型比较简单，一次遍历，对半翻转

	/*
	先split ，然后逐个翻转
	*/
	import java.io.*;
	import java.util.*;
	import java.text.*;
	import java.math.*;
	import java.util.regex.*;
	
	public class Solution {
	        public static void main(String[] args) throws Exception {
	            BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
	            String[] array = in.readLine().split(" ");
	            for (int i = 0; i < array.length; i++) {
	
	                System.out.print(reverse(array[i]) + " ");
	
	            }
	
	        }
	    public static String reverse(String str){
	        char[] array = str.toCharArray();
	        char tmp;
	        for (int i = 0; i < array.length/2; i++) {
	            tmp = array[i];
	            array[i] = array[array.length -1 - i];
	            array[array.length - 1 - i] = tmp;
	        }
	        //Notice that using toString will cause unexpected result
	        return  String.valueOf(array);
	    }
	}
	
题型二：题型二来自leetcode， sky is blue --> blue is sky,这里给出三种方法

	**********************************************************************************
	 *
	 * Given an input string, reverse the string word by word.
	 *
	 * For example,
	 * Given s = "the sky is blue",
	 * return "blue is sky the".
	 *
	 *
	 * Clarification:
	 *
	 * What constitutes a word?
	 * A sequence of non-space characters constitutes a word.
	 * Could the input string contain leading or trailing spaces?
	 * Yes. However, your reversed string should not contain leading or trailing spaces.
	 * How about multiple spaces between two words?
	 * Reduce them to a single space in the reversed string.
	 *
	 *
	 **********************************************************************************/
	public class testRevertString {
	    //效率问题，避免使用正则，如果数据不大，可以用split，但是1000以后呈指数级上升
	    //详情阅读 http://blog.csdn.net/songylwq/article/details/9016609
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
	    //a leetcode solution, did not use split but still using O(N) space
	    public static String revertString2(String s) {
	        StringBuilder builder = new StringBuilder();
	        int j = s.length();
	        for (int i = s.length() - 1 ; i >= 0 ; i--) {
	            if (s.charAt(i) == ' '){
	                j = i;
	            }else if (i == 0 || s.charAt(i -1) == ' '){
	                if (builder.length() != 0){
	                    builder.append(" ");
	                }
	                builder.append(s.substring(i,j));
	            }
	        }
	        return builder.toString();
	    }
	
	
	    public static void reverseStr(char[] A, int start, int end){
	        char tmp;
	        while(start < end){
	            tmp = A[start];
	            A[start] = A[end];
	            A[end] = tmp;
	
	            start++;
	            end--;
	        }
	    }
	
	    //an O(1) space complexity way
	    public static String revertString3(String s) {
	        s.trim();
	        char[] A = s.toCharArray();
	        if(A == null || A.length == 0)return s;
	
	        //reverse all firstly
	        reverseStr(A, 0 , A.length-1);
	        //reverse every single word
	        int j = 0;
	        for (int i = 0; i < A.length; i++) {
	            if(A[i] == ' '){
	                reverseStr(A, j, i-1);
	                j = i+1;
	            }
	            if(i == A.length -1){
	                reverseStr(A, j, i);
	            }
	        }
	        //is there any better solution can remove the duplicated whitespaces?
	        return new String(A).trim().replaceAll(" +" , " ");
	    }
	
	    public static void main(String [] args){
	
	        String[] testStrings = {"hello this is hui   hahaa" ,
	                "  this is    hui  ! ",
	                " "};
	//        String[] testString = {" this is  hui "};
	        for (String str:testStrings){
	                    System.out.println(revertString3(str));
	        }
	
	
	    }
	
	}