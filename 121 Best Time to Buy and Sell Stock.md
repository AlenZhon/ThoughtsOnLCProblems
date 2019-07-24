# 121 Best Time to Buy and Sell Stock

## 题目描述

给定一正整数数列，每个元素表示每一天某件商品的单价。一次买入和卖出视为一笔交易，设计算法求出只能完成一笔交易时，获取的最大利润是多少。

>Say you have an array for which the ith element is the price of a given stock on day i.
>
>If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.
>
>Note that you cannot sell a stock before you buy one.
>
>Example 1:
>
>>Input: [7,1,5,3,6,4]  
>>Output: 5  
>>Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.  Not 7-1 = 6, as selling price needs to be larger than buying price.
>
>Example 2:
>
>>Input: [7,6,4,3,1]  
>>Output: 0  
>>Explanation: In this case, no transaction is done, i.e. max profit = 0.

## 怎么解的

两层循环暴力解其实也可以，但时间复杂度O(n^2)了。有没有O(n)的方法呢？

当然有的了。

题目是要获取最大利润，其实就是要找到最低价格，以及在最低价之后的最高价格。转化为一个寻找数列最小值和在最小值下标之后的最大值问题。两者可以在同一次遍历中实现。

```java
public int maxProfit(int[] prices) {
        int max = 0, minprice = Integer.MAX_VALUE;
        for (int i = 0; i< prices.length; i++) {
            if (prices[i] < minprice) {
                minprice = prices[i];
            }
            if (prices[i] - minprice > max) {
                max = prices[i] - minprice;
            }
        }
        return max;
    }
```
