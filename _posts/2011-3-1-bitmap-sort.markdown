---
layout: post
styles: [syntax]
title: bitmap�㷨��Javaʵ��
---

��������ᡷ����һ���и�����λͼ�㷨���ٶȶԱȣ�

<table>
  <tbody>
    <tr>
      <th></th>
      <th>ϵͳ����</th>
      <th>C++/STL</th>
      <th>C/qsort</th>
      <th>C/λͼ</th>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <th>��ʱ��</th>
      <th>89</th>
      <th>38</th>
      <th>12.6</th>
	  <th>10.7</th>
    </tr>
    <tr>
      <th>����ʱ��</th>
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

JAVAʵ�֣�

{% highlight java linenos=table %}
    public class BitSortTest {  
        private static final int BITSPERWORD = 32;  //����λ��  
        private static final int SHIFT = 5;  
        private static final int MASK = 0x1F;  //5λ�ڱ� 0B11111  
        private static final int N = 10000000;  
        //��int������ģ��λ���飬�ܼ�(1 + N / BITSPERWORD)*BITSPERWORDλ����������N  
        private static int[] a = new int[(1 + N / BITSPERWORD)];  
      
        public static void main(String[] args) {  
            bitsort(new int[]{1, 100, 2, 10000, 9999, 4567, 78902});  
        }  
      
        public static void bitsort(int[] array) {  
            for (int i = 0; i < N; i++)  
                clr(i);   //λ��������λ��0  
            for (int i = 0; i < array.length; i++)  
                set(array[i]);   //�׶�2  
            for (int i = 0; i < N; i++)  
                if (test(i))  
                    System.out.println(i);  
        }  
      
        //��a[i>>SHIFT]�ĵ�(i & MASK)λΪ1��Ҳ����λ����ĵ�iλΪ1  
        public static void set(int i) {  
            a[i >> SHIFT] |= (1 << (i & MASK));  
        }  
      
        //��a[i>>SHIFT]�ĵ�(i & MASK)λΪ0,Ҳ����λ����ĵ�iλΪ0  
        public static void clr(int i) {  
            a[i >> SHIFT] &= ~(1 << (i & MASK));  
        }  
      
        //����λ����ĵ�iλ�Ƿ�Ϊ1  
        public static boolean test(int i) {  
            return (a[i >> SHIFT] & (1 << (i & MASK))) == (1 << (i & MASK));  
        }  
    }  
{% endhighlight %}