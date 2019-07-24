# 123. Best Time to Buy and Sell Stock III

## 题目描述

给定一正整数数列，每个元素表示每一天某件商品的单价。一次买入和卖出视为一笔交易，当最多可完成两次交易的情况下，获取的最大利润是多少。

>Say you have an array for which the ith element is the price of a given stock on day i.
>
>Design an algorithm to find the maximum profit. You may complete at most two transactions.
>
>Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
>
>Example 1:
>
>>Input: [3,3,5,0,0,3,1,4]  
>>Output: 6  
>>Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
>>Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
>
>Example 2:
>
>>Input: [1,2,3,4,5]  
>>Output: 4  
>>Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
>>Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are  
>>engaging multiple transactions at the same time. You must sell before buying again.
>
>Example 3:
>
>>Input: [7,6,4,3,1]  
>>Output: 0  
>>Explanation: In this case, no transaction is done, i.e. max profit = 0.

## 怎么解的

想了一下，觉得在O(n)的情况下可以设两个变量`maxfirst`和`maxsecond`，用于记下目前为止涨价所获得的最大的两次利润。

```java
public int maxProfit(int[] prices) {
        int maxfirst = 0, maxsecond = 0, profit =0;
        for (int i =1; i< prices.length; i++) {
            int diff = prices[i] - prices[i-1];
            if (diff >= 0) {
                maxfirst += diff;
                profit = Math.max(profit, maxfirst +maxsecond);
            } else if (maxfirst >maxsecond) {
                maxsecond = maxfirst;
                maxfirst = 0;
            }
        }
        return profit;
    }
```

做了做发现想法有缺陷。例如[1,2,4,2,5,7,2,4,9,0]，当遍历到7时，存储的两个利润分别是5(2-5-7)和3(1-2-4)，profit是两者之和。但再往后遍历，算法不会记录6(1-2-4-2-5-7)，直接记录下了7(2-4-9)，从而得到7+5=12的答案。

（TODO）
