# 326. Power of Three

## 题目

给定一个整数x，判断它是不是3的幂。要求不用循环/递归。

>Given an integer, write a function to determine if it is a power of three.
>
>**Example 1:**
>
>>Input: 27  
>>Output: true
>
>**Example 2:**
>
>>Input: 0
>>Output: false
>
>**Example 3:**
>
>>Input: 9  
>>Output: true  
>
>**Example 4:**
>
>>Input: 45  
>>Output: false
>
>**Follow up:**
>Could you do it without using any loop / recursion?

## 解法

换底公式。 `3^i = x -> i = log(x)/log(3)`只需判断i是否是整数。时间复杂度取决于Math.log10()，空间O(1)。

```java
return (Math.log10(x)/Math.log10(3) %1 ==0);
```

如果使用`Math.log()`容易出现精度问题。
>This solution is problematic because we start using doubles, which means we are subject to precision errors. This means, we should never use == when comparing doubles. That is because the result of Math.log10(n) / Math.log10(3) could be 5.0000001 or 4.9999999. This effect can be observed by using the function Math.log() instead of Math.log10().
>
>In order to fix that, we need to compare the result against an epsilon.
>
>```java
>return (Math.log(n) / Math.log(3) + epsilon) % 1 <= 2 * epsilon;
>```

## Approach : Integer Limitations

由于是整数，我们可以计算整数范围内最大的3的幂。

>Integer.MAX_VALUE = 2^31 -1 = 2147483647  
>log_3 Integer.MAX_VALUE = 19.56...  
>3^19 = 1162261467

这个数能被整数范围内所有3的整数幂整除。

```java
return n > 0 && 1162261467 % n == 0;
```

时间复杂度O(1) , 空间O(1)。
