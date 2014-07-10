---
layout: post
title: "[leetcode]climb stairs"
description: ""
category: 
tags: [leetcode, java, fibonacci]
---
{% include JB/setup %}

###Problem:Climb Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Solution 1: Recursive**

f(n) = f(n-1) + f(n-2) 很显然这是一个斐波那契数列问题(1 1 2 3 5..)，只不过初始条件是n=2 

    public static int fibonacci_recursive(int n){
        if (n == 1){
            return 1;
        }
        if (n == 2){
            return 2;
        }
        return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2);
    }

递归算法明显超时，原因是每个f(n)被计算了多次，随着n的增长，运算时间很可怕,计算n=50在rmbp上花了将近一分钟的时间

**Solution 2: Iteration**

    public static long fibonacci_iteration(long n){
        long current = 1;
        long prev = 0;
        for (long i = 0; i <n; i++) {
            long tmp = current;
            current = current + prev;
            prev = tmp;
        }

        return current;

    }


**算法效率对比：
**
<table border="1">
	    <tr>
        <td>Solution</td>
        <td>Caculate Result</td>
        <td>Time cost(n = 50)</td>
   	    </tr>
   	   	<tr>
        <td>Recursive</td>
         <td>20365011074</td>
         <td>42s</td>
   	    </tr>
   	    <td>Iteration</td>
         <td>20365011074</td>
         <td>~0s</td>
   	    </tr>
</table>

