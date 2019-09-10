# 342. Power of Four

## 题目

给定一个整数，判断这个整数是否是4的幂。要求最好不要用循环/递归。

>Given an integer (signed 32 bits), write a function to check whether it is a power of 4.
>
>**Example 1:**
>
>>Input: 16  
>>Output: true  
>
>**Example 2:**
>
>>Input: 5  
>>Output: false  
>
>**Follow up:** Could you solve it without loops/recursion?

## 解法

换底公式。这个解法的主要缺点就是时间复杂度不好分析。

```java
return num>0 && Math.log10(num) / Math.log10(4) %1 ==0;
```

Power of Three 里的另一种方法直接使用会有问题，因为2的幂也可以除4^15 = 1073741824
不过既然是4，可能和位运算也有关系。#231里有一个计算Power of Two的骚方法 `n&(n-1) == 0`。既然是4的幂，肯定也是2的幂，所以考虑再添加一个判断条件将是2的幂而非4的幂的数去掉。

比如 2 = (10)_2 8 = (1000)_2, 32 = (100000)_2，发现这些要去掉的数它的1是在偶数位上。构造mask 01010101010101010101010101010101 = 0x55555555，`mask & num != 0`

```java
 return num > 0 && ((num & (num-1)) == 0) && (((num & 0x55555555) != 0);
```

或是对mask按位取反，得到0xaaaaaaaa

```java
 return num > 0 && ((num & (num-1)) == 0) && (((num & 0xaaaaaaaa) == 0);
```

## Notes

*#231 Power of Two*  
*#326 Power of Three*  
