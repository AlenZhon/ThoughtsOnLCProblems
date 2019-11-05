# 754. Reach a Number

## 题目

给定整数target，从数轴的原点0出发，第n步可向左或向右走n格，求最少可以走几步就能到达target。

>You are standing at position 0 on an infinite number line. There is a goal at position target.
>
>On each move, you can either go left or right. During the n-th move (starting from 1), you take n steps.
>
>Return the minimum number of steps required to reach the destination.
>
>**Example 1:**
>
>>Input: target = 3  
>>Output: 2  
>>Explanation:  
>>On the first move we step from 0 to 1.  
>>On the second step we step from 1 to 3.  
>
>**Example 2:**
>
>>Input: target = 2  
>>Output: 3  
>>Explanation:  
>>On the first move we step from 0 to 1.  
>>On the second move we step  from 1 to -1.  
>>On the third move we step from -1 to 2.
>
>**Note:**
>target will be a non-zero integer in the range `[-10^9, 10^9]`.

## 解法

数学问题。在连加式子`1 + 2 + 3 + ... + k > target`中把加号变减号，使得两边取等。大概的思路如下：

```java
首先由于正负数的对称性，只需考虑target大于0的情况。  

1. 逐项加和使得 sum = 1 + 2 + 3 + ... + step >= target

2. 如果sum == target ，直接返回step。

3. 否则sum > target， 令 diff = sum - target

  3.1 如果 diff 是偶数， 只需将连加式中 diff / 2 项置为负。
  3.2 如果 diff 是奇数， 自加step直到diff变为偶数。
```

例如  
target = 4 经过第1步后 sum = 6, step = 3  
diff = 6 - 4 = 2, 所以只需将 2 / 2 = 1 置为负，即4 = -1 + 2 + 3

又如  
target = 5 经过第1步后 sum = 6, step = 3  
diff = 6 - 5 = 1 为奇数  
自增step, sum = 10 , step = 4  
diff = 10 - 5 = 5 为奇数  
自增step, sum = 15 , step = 5
diff = 15 - 5 = 10 , 将10 / 2 = 5设为负，即 5 = 1 + 2 + 3 + 4 - 5

```java
public int reachNumber(int target) {
        target = Math.abs(target);
        int step = 0, sum = 0;
        while (sum < target)
            sum += ++step;
        while ((sum - target) % 2 != 0)
            sum+= ++step;
        return step;
    }
```

更狠的在这里

```java
public int reachNumber(final int target) {
        final int n1 = (int)Math.ceil((-1 + Math.sqrt(1 + 8.0 * Math.abs(target))) / 2);
        final int sum = n1 * (n1 + 1) / 2;

        if (sum % 2 == Math.abs(target) % 2) {
            return n1;
        }

        return n1 + (n1 % 2 == 0 ? 1 : 2);
    }
```
