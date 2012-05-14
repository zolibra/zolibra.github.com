---
layout: post
styles: [syntax]
title: bitmap算法的Java实现
---

《编程珠玑》，第一章中给出了位图算法，速度对比：

<table>
  <tbody>
    <tr>
      <th></th>
      <th>系统排序</th>
      <th>C++/STL</th>
      <th>C/qsort</th>
      <th>C/位图</th>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <th>总时间</th>
      <th>89</th>
      <th>38</th>
      <th>12.6</th>
	  <th>10.7</th>
    </tr>
    <tr>
      <th>计算时间</th>
      <th>79</th>
      <th>28</th>
      <th>2.4</th>
	  <th>0.5</th>
    </tr>
      <th>MB</th>
      <th>0.8</th>
      <th>70</th>
      <th>4</th>
	  <th>1.25</th>	
  </tbody>
</table>

JAVA实现：

{% highlight java linenos=table %}
    public class BitSortTest {  
        private static final int BITSPERWORD = 32;  //整数位数  
        private static final int SHIFT = 5;  
        private static final int MASK = 0x1F;  //5位遮蔽 0B11111  
        private static final int N = 10000000;  
        //用int数组来模拟位数组，总计(1 + N / BITSPERWORD)*BITSPERWORD位，足以容纳N  
        private static int[] a = new int[(1 + N / BITSPERWORD)];  
      
        public static void main(String[] args) {  
            bitsort(new int[]{1, 100, 2, 10000, 9999, 4567, 78902});  
        }  
      
        public static void bitsort(int[] array) {  
            for (int i = 0; i < N; i++)  
                clr(i);   //位数组所有位清0  
            for (int i = 0; i < array.length; i++)  
                set(array[i]);   //阶段2  
            for (int i = 0; i < N; i++)  
                if (test(i))  
                    System.out.println(i);  
        }  
      
        //置a[i>>SHIFT]的第(i & MASK)位为1，也就是位数组的第i位为1  
        public static void set(int i) {  
            a[i >> SHIFT] |= (1 << (i & MASK));  
        }  
      
        //置a[i>>SHIFT]的第(i & MASK)位为0,也就是位数组的第i位为0  
        public static void clr(int i) {  
            a[i >> SHIFT] &= ~(1 << (i & MASK));  
        }  
      
        //测试位数组的第i位是否为1  
        public static boolean test(int i) {  
            return (a[i >> SHIFT] & (1 << (i & MASK))) == (1 << (i & MASK));  
        }  
    }  
{% endhighlight %}