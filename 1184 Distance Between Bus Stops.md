# 1184. Distance Between Bus Stops

## 题目

一辆环线公交车总共有n个站，用一个数组表示站与站之间的距离。现在给定两个公交车站，公交车可以按顺时针路线，也可逆时针路线。问两个公交车站之间的最短距离是多少？

>A bus has n stops numbered from 0 to n - 1 that form a circle. We know the distance between all pairs of neighboring stops where distance[i] is the distance between the stops number i and (i + 1) % n.
>
>The bus goes along both directions i.e. clockwise and counterclockwise.
>
>Return the shortest distance between the given start and destination stops.
>
>**Example 1:**
>
>>Input: distance = [1,2,3,4], start = 0, destination = 1  
>>Output: 1  
>>Explanation: Distance between 0 and 1 is 1 or 9, minimum is 1.
>
>**Example 2:**
>
>>Input: distance = [1,2,3,4], start = 0, destination = 2  
>>Output: 3  
>>Explanation: Distance between 0 and 2 is 3 or 7, minimum is 3.
>
>**Example 3:**
>
>>Input: distance = [1,2,3,4], start = 0, destination = 3  
>>Output: 4  
>>Explanation: Distance between 0 and 3 is 6 or 4, minimum is 4.
>
>**Constraints:**
>
> - 1 <= n <= 10^4
> - distance.length == n
> - 0 <= start, destination < n
> - 0 <= distance[i] <= 10^4

## 解法

约束条件保证了不会溢出。所以计算数组元素之和，再算顺时针路线距离，两者相减即可得到逆时针路线的距离。时间复杂度O(n)。

```java
public int distanceBetweenBusStops(int[] distance, int start, int destination) {
        int sum = 0, clockwise = 0;
        if (start == destination) return 0;
        if (start > destination) {
            int temp = start;
            start = destination;
            destination = temp;
        }
        for (int i = 0; i< distance.length; i++){
            sum+= distance[i];
            if (i >= start && i < destination)
                clockwise += distance[i];
        }
        return Math.min(sum - clockwise, clockwise);
    }
```
