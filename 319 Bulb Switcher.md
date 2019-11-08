# 319. Bulb Switcher

## 题目

有n盏灯默认都是关闭状态，对它们进行n次操作。第一次操作打开每1盏灯；第二次操作时每两盏灯改变一盏灯的状态；第i次操作时，改变每i盏灯的状态。问进行n次操作后有多少盏灯还亮着。

>There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the i-th round, you toggle every i bulb. For the n-th round, you only toggle the last bulb. Find how many bulbs are on after n rounds.
>
>Example:
>
>>Input: 3  
>>Output: 1  
>>Explanation:  
>>At first, the three bulbs are [off, off, off].  
>>After first round, the three bulbs are [on, on, on].  
>>After second round, the three bulbs are [on, off, on].  
>>After third round, the three bulbs are [on, off, off].  
>>
>>So you should return 1, because there is only one bulb is on.

## 解法

一个脑筋急转弯的问题。

对于第i盏灯，它改变状态的次数和它的因子个数有关。如果它的因子个数是奇数，那么奇数次改变状态之后它就是亮的。

实际上，只有完全平方数的因子个数是奇数。所以只需计算n以内的完全平方数个数即可。

```java
  return (int)Math.sqrt(n);
```
