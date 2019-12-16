# 1217. Play with Chips

## 题目

现在有一堆芯片随机摆成一排，第i个芯片摆在`chips[i]`的位置上。  
对于任意一个芯片，你可以对其进行任意次数（包括0次）的如下两种操作：

- 花费1成本将此芯片向左/向右移动一格。
- 花费0成本将此芯片向左/向右移动两格。

给定`chips`数组表示当前芯片所在的位置，问最少需要花费多少成本可将所有芯片移动到同一个位置（这一排里的任意一个位置）。

>There are some chips, and the i-th chip is at position `chips[i]`.
>
>You can perform any of the two following types of moves any number of times (possibly zero) on any chip:
>
> - Move the i-th chip by 2 units to the left or to the right with a cost of 0.
> - Move the i-th chip by 1 unit to the left or to the right with a cost of 1.
>
>There can be two or more chips at the same position initially.
>
>Return the minimum cost needed to move all the chips to the same position (any position).
>
>**Example 1:**
>
>>Input: chips = [1,2,3]  
>>Output: 1  
>>Explanation: Second chip will be moved to positon 3 with cost 1. First chip will be moved to position 3 with cost 0. Total cost is 1.
>
>**Example 2:**
>
>>Input: chips = [2,2,2,3,3]  
>>Output: 2  
>>Explanation: Both fourth and fifth chip will be moved to position two with cost 1. Total minimum cost will be 2.
>
>**Constraints:**
>
> - `1 <= chips.length <= 100`
> - `1 <= chips[i] <= 10^9`

## 解法

首先要看懂题目。  
chips数组里存的是所有芯片的初始位置。由题意，移动2格不计成本，那所有位置就自动按照奇偶性划分为了两个格子，不妨设为位置0和位置1，所有芯片都可以通过向左移动若干次2格到达位置0/位置1。

那么，问题就直接解决了。如果所有芯片都在同一个位置上（比如全在位置0）那么根本不用成本。否则，把少的那一堆芯片移动到多的那一堆上。

```java
public int minCostToMoveChips(int[] chips) {
        int[] pair = new int[2];
        for (int i = 0; i < chips.length; i++)
            pair[chips[i] & 1]++;
        if ((pair[0] ==0 && pair[1] > 0) || (pair[0] > 0 && pair[1] == 0)) return 0;
        return Math.min(pair[0], pair[1]);
    }
```
