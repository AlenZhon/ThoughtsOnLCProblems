# 598. Range Addition II

## 题目

一个 `m*n` 的零矩阵`M`，对该矩阵进行若干步迭代更新操作。每一次操作定义为`0 <= i < a and 0 <= j < b`的所有`M[i][j]`自增1。现在给定m,n和操作步骤，计算操作结束时矩阵中最大元素的个数，并返回。

>Given an `m * n` matrix `M` initialized with all 0's and several update operations.
>
>Operations are represented by a 2D array, and each operation is represented by an array with two positive integers `a` and `b`, which means `M[i][j]` should be added by one for all `0 <= i < a and 0 <= j < b`.
>
>You need to count and return the number of maximum integers in the matrix after performing all the operations.
>
>Example 1:
>
>>Input:  
>>m = 3, n = 3  
>>operations = [[2,2],[3,3]]  
>>Output: 4  
>>Explanation:  
>>Initially, M =
>>[[0, 0, 0],
>> [0, 0, 0],
>> [0, 0, 0]]
>>
>>After performing [2,2], M =
>>[[1, 1, 0],[1, 1, 0], [0, 0, 0]]
>>
>>After performing [3,3], M =
>>[[2, 2, 1], [2, 2, 1], [1, 1, 1]]
>>
>>So the maximum integer in M is 2, and there are four of it in M. So return 4.
>
>**Note:**
>
> 1. The range of m and n is [1,40000].
The range of a is [1,m], and the range of b is [1,n].
> 2. The range of operations size won't exceed 10,000.

## 解法

看懂题目之后就发现是一个水题。由于自增的操作都是从矩阵的左上角开始算，只需计算每个操作时最小的维数即可。

时间复杂度和二维数组`operation`的行数线性相关。空间复杂度O(1)。

```java
public int maxCount(int m, int n, int[][] ops) {
        int minA = m, minB = n;
        for (int i = 0; i< ops.length; i++) {
            minA = Math.min(ops[i][0], minA);
            minB = Math.min(ops[i][1], minB);
        }
        return minA * minB;
    }
```
