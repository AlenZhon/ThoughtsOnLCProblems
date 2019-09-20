# 441. Arranging Coins

## 题目

把一堆硬币摆成阶梯形状，第k行恰好有k个硬币。给定硬币个数，求能摆出多少行。

>You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.
>
>Given n, find the total number of full staircase rows that can be formed.
>
>n is a non-negative integer and fits within the range of a 32-bit signed integer.
>
>**Example 1:**
>
>>n = 5
>>
>>The coins can form the following rows:  
>>¤  
>>¤ ¤  
>>¤ ¤  
>>
>>Because the 3rd row is incomplete, we return 2.
>
>**Example 2:**
>
>>n = 8
>>
>>The coins can form the following rows:  
>>¤  
>>¤ ¤  
>>¤ ¤ ¤  
>>¤ ¤
>>
>>Because the 4th row is incomplete, we return 3.

## 解法

一个等差数列求和的题目。
一开始还想预先保存每个阶梯的硬币数再遍历求和，结果Time Limit Exceeded。

直接求根公式走起来，注意用`long`避免overflow就行。时间复杂度根据`Math.sqrt()`决定。
