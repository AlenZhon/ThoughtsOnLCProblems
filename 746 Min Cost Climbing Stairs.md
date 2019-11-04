# 746. Min Cost Climbing Stairs

## 题目

要上一段台阶，一步可以走一级，或者可以跨两级台阶。现在给出登上每级台阶所需要的cost。求出从最低点登到最高一级台阶的最小cost方法。

>On a staircase, the `i-th` step has some non-negative cost `cost[i]` assigned (0 indexed).
>
>Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.
>
>**Example 1:**
>
>>Input: cost = `[10, 15, 20]`  
>>Output: 15  
>>Explanation: Cheapest is start on cost[1], pay that cost and go to the top.
>
>**Example 2:**
>
>>Input: cost = `[1, 100, 1, 1, 1, 100, 1, 1, 100, 1]`
>>Output: 6  
>>Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].
>
>**Note:**
>
> - cost will have a length in the range [2, 1000].
> - Every cost[i] will be an integer in the range [0, 999].

## 解法

肯定是一个动态规划的问题了。如果已经登上了第i级台阶(`i>=2, i in [0, n]`)，那么目前最小的cost是 `f(i) = cost[i] + min(f(i - 1), f(i - 2))` ，将`f1, f2`分别设为 `cost[0], cost[1]` ，迭代求解，最后取`min(f1, f2)`。

```java
 public int minCostClimbingStairs(int[] cost) {
        int f1 = cost[0], f2 = cost[1];
        for (int i = 2; i< cost.length; i++) {
            int curCost = cost[i] + Math.min(f1, f2);
            f1 = f2;
            f2 = curCost;
        }
        return Math.min(f1, f2);
    }
```

时间复杂度O(n)，空间复杂度O(1)。
