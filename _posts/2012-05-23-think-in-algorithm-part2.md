---
layout: post
title: "Think in algorithm part.2"
description: ""
category: 
tags: []
---
{% include JB/setup %}
Programming Pearls.2nd Chapter
=============================
There is an awsome algorithm mentioned in this Chapter:
if you want to reverse `ABCdefgh` to `defghABC` ,how do you do that?

Maybe most of us will implement as like this:

    void reverse(char [] arr , int len, int m){
    char [3] temp = new char[3];
    //copy ABC to temp array
	    for(int i = 0;i<m:i++){
	    temp[i] = arr[i];
        }
        //move defgh to len - m pos
        for(int i = m; i < len; i++){ 
            arr[i-m] = arr[i]; 
        }
        //append the temp arr to the original arr
        for(int i = 0; i < m; i++){ 
            arr[len-m+i] = temp[i]; 
        }
    }
	
but maybe we only need a hand turn over:
![hand turn](http://zolibra.github.io/assets/images/reverse.png)

so we only need:

    reverse(0 , i-1);	/* CBAdefgh */
    reverse(i , n-1);	/* CBAhgfed */
    reverse(0 , n-1);	/* defghABC */
	
C implement:

    void reverse(char [] arr, int start, int end){ 
        int mid = (start + end) / 2; 
        for(int s = start, i = 1; i < mid; s++, i++){ 
            char temp = arr[s]; 
            arr[s] = arr[end-i]; 
            arr[end-i] = temp; 
        } 
    } 
     	

	
	