---
layout: post
title: "[CA]LastIndexOfSubString"
description: ""
category: 
tags: [DP,LCS,String,MJ]
---
{% include JB/setup %}

given StringA "aabbcd", and StringB "bc", find the last index of StringB, in this cases it is 3.

	"aabbaacc" --> "aa" is 4
	"abcdefefefeefcc" --> "ef" is 11


方法一：朴素算法，算法复杂度O(mn),m 是A的长度， n是B的长度


    public boolean isEquel(char[] a , char[] b){
        for (int i = 0; i < a.length; i++){
            if (a[i] != b[i])return false;
        }
        return true;
    }
    //需要一个m的空间保存从A中截取的待比较字符串
    public int BruteForce1(char[] A, char[] B){
        if (A == null||B == null) return -1;
        if (A.length < B.length) return -1;
        if (A.length == B.length)return isEquel(A,B)?0:-1;

        char[] temp = new char[B.length];

        for (int i = A.length - B.length; i>=0; i--){
            System.arraycopy(A,i,temp,0,temp.length);
            if(isEquel(temp,B))return i;
        }
        return -1;
    }

方法二：不借助中间变量

    public int BruteForce2(char[] A, char[] B){
        int lenA = A.length;
        int lenB = B.length;
        for(int i=lenA - lenB; i>=0; i--) {
            int k = i; // k point to next A pos
            for(int j=0; j<lenB; j++) {
                if(A[k] != B[j]) {
                    break;
                }else {
                    k++;// point to next pos
                    if(j == lenB-1) {
                        return i;
                    }
                }
            }
        }
        return -1;
    }    

方法三：KMP
 
	public class LastIndexOfSubString {
	
	    public int[] computePrefix(char[] P){
	        int m = P.length;
	        int pi[] = new int[m];
	        pi[0] = 0;
	        int k = 0;
	        for (int i = 1; i < m; i++) {
	            while ( k>0 && P[k] != P[i]) {
	                k = pi[k - 1];
	            }
	            if (P[k] == P[i])k++;
	            pi[i] = k;
	        }
	        System.out.println(Arrays.toString(pi));
	        return pi;
	    }
	
	    public int kmpMatch(char[] T, char[] P){
	        int n = T.length;
	        int m = P.length;
	        int[] pi = computePrefix(P);
	        int q = 0;
	        for (int i = 0; i < n ; i++) {
	            while(q > 0 && P[q] != T[i]) {
	                q = pi[q -1];
	            }
	            if(P[q] == T[i])
	                q++;
	            if(q == m) {
	                return i-m+1;
	            }
	        }
	        return -1;
	    }
	
	
	    public static void main(String[] args) {
	        StringBuffer a = new StringBuffer("badcbadcba cba bb aa");
	        StringBuffer b = new StringBuffer("badcba");
	        LastIndexOfSubString lios = new LastIndexOfSubString();
	        //just reverse the input and matching from head to tail
	        int reverseIndex = lios.kmpMatch(a.reverse().toString().toCharArray(),
	                b.reverse().toString().toCharArray());
	        int index = a.length() - b.length() - reverseIndex;
	        System.out.println(index);
	    }
	
	}

思考： 如何调整KMP算法使得不需要reverse string 直接匹配？