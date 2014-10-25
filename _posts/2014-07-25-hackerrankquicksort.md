---
layout: post
title: "[hackerrank]QuickSort"
description: ""
category: 
tags: [hackerrank,sort]
---
{% include JB/setup %}

###QuickSort Part1: Partition

Guideline - In this challenge, you do not need to move around the numbers 'in-place'. This means you can create 2 lists and combine them at the end.

Sample Input

	5
	4 5 3 7 2
Sample Output
	
	3 2 4 5 7

My impelemetation, using helper arraylist:
	
	import java.util.*;
	public class Solution {
	
	    static void partition(int[] ar) {
	        int p = ar[0];
	        List smaller = new ArrayList();
	        List bigger = new ArrayList();
	
	        for(int j = 1; j<ar.length;j++){
	            if(ar[j] <= p){
	                smaller.add(ar[j]);
	            }else{
	                bigger.add(ar[j]);
	            }
	        }
	        for(int j = 0; j< smaller.size();j++){
	            ar[j] = (Integer)smaller.toArray()[j];
	        }
	        ar[smaller.size()] = p;
	        for(int j = 0; j < bigger.size();j++){
	            ar[smaller.size()+j+1] = (Integer)bigger.toArray()[j];
	        }
	        printArray(ar);
	    }
	
	    static void printArray(int[] ar) {
	        for(int n: ar){
	            System.out.print(n+" ");
	        }
	        System.out.println("");
	    }
	
	    public static void main(String[] args) {
	        Scanner in = new Scanner(System.in);
	        int n = in.nextInt();
	        int[] ar = new int[n];
	        for(int i=0;i<n;i++){
	            ar[i]=in.nextInt();
	        }
	        partition(ar);
	    }
	}
	
虽然通过了test cases 但是提示有不安全的编译的问题：

	Note: Solution.java uses unchecked or unsafe operations.
	Note: Recompile with -Xlint:unchecked for details.

This is because you are using ArrayList with raw type. And you are adding a specific type to it.

Raw type ArrayList would expect element of type Object. If you add any other type, then Compiler would not know exactly what type you are storing. So, it gives you unchecked or unsafe operations to warn you that you might be doing something wrong.

You should better create a Generic ArrayList:-

        List<Integer> smaller = new ArrayList<Integer>();
        List<Integer> bigger = new ArrayList<Integer>();
        

###QuickSort Part2: Sorting
Hackerrank给出的这个quicksort算法其实并不是标准的算法导论的方法，更像是一种归并排序的逆方法，没有用到交换而是借助数组完成元素的分配。

Sample Input

	7 
	5 8 1 3 7 9 2

Sample Output 

	2 3 
	1 2 3 
	7 8 9 
	1 2 3 5 7 8 9
实现如下：

	    static int hackerrankPartition(int[] ar, int p, int r) {
	        int x = ar[p];
	        List<Integer> smaller = new ArrayList<Integer>();
	        List<Integer> bigger = new ArrayList<Integer>();
	
	        for(int j = p+1; j<=r;j++){
	            if(ar[j] <= x){
	                smaller.add(ar[j]);
	            }else{
	                bigger.add(ar[j]);
	            }
	        }
	        int j;
	        for(j = 0; j< smaller.size();j++){
	            ar[p+j] = (Integer)smaller.toArray()[j];
	        }
	        ar[p+smaller.size()] = x;
	        for(j = 0; j < bigger.size();j++){
	            ar[smaller.size()+p+j+1] = (Integer)bigger.toArray()[j];
	        }
	        return p+smaller.size();
	    }
	    static void hackerrankQuickSort(int[] ar, int p, int r){
	        if(p<r){
	            int q = hackerrankPartition(ar,p,r);
	            hackerrankQuickSort(ar,p,q-1);
	            hackerrankQuickSort(ar,q+1,r);
	            printArray(ar, p, r);
	        }
	    }
	
	    static void quickSort(int[] ar) {
	//        realQuickSort(ar, 0 ,ar.length-1);
	        hackerrankQuickSort(ar, 0 ,ar.length-1);
	    }
	
	    static void printArray(int[] ar, int p, int r) {
	        for(int i = p; i <=r;i++){
	            System.out.print(ar[i]+" ");
	        }
	        System.out.println("");
	    }
标准的做法是通过swap来完成subarry的排序，两种方法在subarray的输出序列上存在差异

以下是标准实现：

    //5 8 1 3 7 9 2 主元为A[p] = 5
    static int partition2(int[]ar, int p, int r){
        int x = ar[p];
        int i = p;
        for(int j = p+1; j<=r;j++){
            if(ar[j]<=x){
                i++;
                //swap
                int tmp = ar[i];
                ar[i] = ar[j];
                ar[j] = tmp;
            }
        }
        //swap
        int tmp = ar[p];
        ar[p] = ar[i];
        ar[i] = tmp;
        return i;
    }
    static void realQuickSort(int[] ar, int p, int r){
        if(p<r){
            int q = partition2(ar,p,r);
            realQuickSort(ar,p,q-1);
            realQuickSort(ar,q+1,r);
            for(int i=p;i<=r;i++)
                System.out.print(ar[i] + " ");
            System.out.println();
        }
    }
[QuickSort More](http://en.wikipedia.org/wiki/Quicksort#In-place_version hope this link helps.)