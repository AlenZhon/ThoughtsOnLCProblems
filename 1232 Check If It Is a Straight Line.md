# 1232. Check If It Is a Straight Line

## 题目

二维平面上给定一堆点，问这些点是不是都在同一条直线上。

>You are given an array `coordinates`, `coordinates[i] = [x, y]`, where `[x, y]` represents the coordinate of a point. Check if these points make a straight line in the XY plane.
>
>**Example 1:**
>
>>Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]  
>>Output: true  
>
>**Example 2:**
>
>>Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]  
>>Output: false  
>
>**Constraints:**
>
> - 2 <= `coordinates.length` <= 1000
> - `coordinates[i].length` == 2
> - -10^4 <= `coordinates[i][0], coordinates[i][1]` <= 10^4
> - `coordinates` contains no duplicate point.

## 解法

自信题目。

```java
public boolean checkStraightLine(int[][] co) {
        if (co.length == 2) return true;
        int[] p = co[0];
        int[] q = co[1];
        for (int i = 2; i< co.length; i++){
            int[] arr = co[i];
            if ((arr[1] - p[1]) * (p[0] - q[0]) != (arr[0] - p[0]) * (p[1] - q[1])) return false;
        }
        return true;
    }
```
