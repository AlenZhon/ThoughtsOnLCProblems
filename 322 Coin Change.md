# 322. Coin Change

## 题目

给定一个数组表示你现在拥有的硬币种类，假设每种硬币的个数不限。现在需要让你找amount块钱，最少使用多少个硬币即可满足要求？（如果无法通过手头上的硬币凑齐amount块钱则返回-1）

>You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.
>
>**Example 1:**
>
>>Input: coins = [1, 2, 5], amount = 11  
>>Output: 3  
>>Explanation: 11 = 5 + 5 + 1  
>
>**Example 2:**
>
>>Input: coins = [2], amount = 3  
>>Output: -1  
>
>**Note:**
>You may assume that you have an infinite number of each kind of coin.

## 解法

由于找钱的问题可以划分为找若干个子问题的最小值，所以考虑用动态规划的思路走。设目前硬币种类为`(c1, c2, c3, cn)`，要凑齐`amount`块钱所需的最少硬币个数为`F(amount)`，那么这个个数就是以下若干个值的最小值
`(F(amount - c1), F(amount - c2), F(amount - c3), ..., F(amount - cn))`，其中括号内的值均不小于0。初始值F(0) = 0。

由于重复用到了多次之前的值，使用一个int[]数组用于存储之前已经计算过的F()值，减少递归的次数。注意`change()`方法的第三个if，判断条件为不等于零，其中包含了大于零（能找钱）和等于-1（不能找钱）的情况。

时间复杂度O(amount * coins.length)， 空间复杂度O(amount)。

```java
public int coinChange(int[] coins, int amount) {
        if (amount < 1) return 0;
        return change(coins, amount, new int[amount]);
    }
    private int change(int[] coins, int remain, int[] count){
        if (remain < 0) return -1;
        if (remain == 0) return 0;
        if (count[remain - 1] != 0) return count[remain - 1];
        int min = Integer.MAX_VALUE;
        for (int c : coins){
            int resCount = change(coins, remain - c, count);
            if (resCount >=0 && resCount < min)
                min = 1 + resCount;
        }
        count[remain - 1] = (min == Integer.MAX_VALUE) ? -1 : min;
        return count[remain - 1];
    }
```

### 另一种解法 (DP bottom-up)

```java
public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++)
            for (int j = 0; j < coins.length; j++)
                if (coins[j] <= i)
                    dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
        return dp[amount] == amount + 1 ? -1 : dp[amount];
    }
```

时间复杂度O(amount * coins.length)， 空间复杂度O(amount)。(15ms)

1ms的方法是用全局变量res记录最少次数。预先对coins排序，然后在比较前计算是否能被当前coin整除。

```java
int res = Integer.MAX_VALUE;
    public int coinChange(int[] coins, int amount) {
        if(coins == null || coins.length == 0) return -1;
        if(amount == 0) return 0;
        Arrays.sort(coins);
        count(coins, amount, coins.length -1, 0);

        return res == Integer.MAX_VALUE ? -1 : res;
    }

    private void count(int[] coins, int amount, int index, int cur){
        if(index < 0) return;
        int val = amount % coins[index];
        int count = amount / coins[index];
        if(val == 0){
            res = Math.min(res, cur + count);
            return;
        }

        for(int i = count; i >= 0; i--){
            int restAmount = amount - i * coins[index];
            if (cur + i >= res-1) break;
            count(coins, restAmount, index-1, cur+i);
        }

        return;

    }
```
