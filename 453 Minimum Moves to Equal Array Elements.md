# 453. Minimum Moves to Equal Array Elements

## 题目

对于一个数组，定义“一步”的操作为： 选定某个元素保持，对其他所有元素自增1。 现在给定一个整数数组，对该数组进行若干步操作使得这个数组的所有元素相等。求出最小的操作步数。

>Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.
>
>**Example:**
>
>>Input:  
>>[1,2,3]
>>
>>Output:  
>>3
>>
>**Explanation:**
>Only three moves are needed (remember each move increments two elements):
>`[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]`

## 解法

审题结束觉得这个问题似乎是一个数学问题。对于题目给定的自增操作，容易得到一个性质：对于数组中的最小元素，按照最小操作步数进行操作时始终保持最小（或最小之一），直到所有元素相等。下面用性质一表示。

因为每次操作时，我们总是固定目前数组里的最大元素`currMax`，其他所有元素自增。即使操作前`currMax`只比最小元素`minNum`大1，操作结束后两者也只是相等，`minNum`还是最小元素之一。

假设原数组所有元素个数为`n`，元素之和是`sum`，最小元素为`minNum`，经过最小的操作次数`m`之后，所有元素均变成`x`。则有等式恒成立：

`sum + m * (n - 1) = x * n`

由性质一，我们又可以得到： `minNum + m = x`

两者联立消去未知量`x`，有 `sum - minNum * n = m`

原题目即转化为找数组里最小元素，并计算每个元素与最小元素差值之和的问题。

```java
public int minMoves(int[] nums) {
        int minNum = Integer.MAX_VALUE, ans = 0;
        for (int n: nums)
            if (n < minNum) minNum =n;
        for (int n: nums)  //avoid sum overflow
            ans += n - minNum;
        return ans;
    }
```
