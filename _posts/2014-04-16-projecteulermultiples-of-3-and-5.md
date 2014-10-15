---
layout: post
title: "[projectEuler+]Multiples of 3 and 5"
description: ""
category: 
tags: [algorithsm]
---
{% include JB/setup %}

If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Find the sum of all the multiples of 3 or 5 below 1000.

利用等差数列求和公式使得时间复杂度为O(1)

	public class Solution {
	
	    public static long count(long num, int diff){
	        //等差数列求和公式
	        return  --num / diff * diff * (1 + num / diff) /2;
	
	    }
	
	    public static void main(String[] args) {
	        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
	        try{
	            BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
	            int N = Integer.parseInt(in.readLine());
	            for(int i = 0; i<N; i++){
	                long sum = 0;
	                long a = Long.parseLong(in.readLine());
	                sum = count(a,3)+count(a,5)-count(a,15);
	                System.out.println(sum);
	            }
	        }catch(IOException e){
	
	        }
	    }
	}