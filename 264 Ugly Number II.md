# 264. Ugly Number II

## 题目

给定正整数n(n<=1690)，求第n个丑数。除了第一个丑数1，其他丑数的定义是只含有质因子2，3，5的数。

>Write a program to find the n-th ugly number.
>
>Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.
>
>**Example:**
>
>>Input: n = 10  
>>Output: 12  
>>Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
>
>**Note:**
>
> 1. 1 is typically treated as an ugly number.
> 2. `n` does not exceed 1690.

## 解法

遍历正整数判断是否是丑数，时间复杂度肯定噌噌噌往上走，所以舍弃。一看给定了提示`n<=1690`，想到的方法就是打表。

实际上，分配一个数组用于存放现有所有丑数，新加入的丑数必定是之前丑数的2，3，5倍。指定3个指针，分别指向不大于目前最大丑数1/2，1/3，1/5的位置，每次比较这三个位置取最小值，自增相应指针。最后输出相应位置的丑数。

```java
public int nthUglyNumber(int n) {
        int[] table = new int[1690];
        table[0] =1;
        int k = 0, p2 = 0, p3 = 0, p5 = 0;
        while (k < n-1) {
            table[++k] = Math.min(Math.min(2*table[p2], 3*table[p3]), 5*table[p5]);
            if (table[k] == 2* table[p2]) p2++;
            if (table[k] == 3* table[p3]) p3++;
            if (table[k] == 5* table[p5]) p5++;
        }
        return table[n-1];
    }
```
