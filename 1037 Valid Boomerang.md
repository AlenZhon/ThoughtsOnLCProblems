# 1037. Valid Boomerang

## 题目

给定三个点的坐标，问这三点是否形成一个boomerang。
一个boomerang表示三点互不相同且不在一条直线上。

>A boomerang is a set of 3 points that are all distinct and **not** in a straight line.
>
>Given a list of three points in the plane, return whether these points are a boomerang.
>
>Example 1:
>
>>Input: [[1,1],[2,3],[3,2]]  
>>Output: true
>>
>Example 2:
>
>>Input: [[1,1],[2,2],[3,3]]  
>>Output: false  
>
>**Note:**
>
> - points.length == 3
> - points[i].length == 2
> - 0 <= points[i][j] <= 100

## 解法

按照题目意思，只需判断三个点围成的面积是否为0即可。

给定三个点的坐标(x1, y1),(x2, y2),(x3, y3)
围成的面积为 abs(x1(y2 - y3) + x2(y3 - y1) + x3(y1 - y2)) / 2.

所以只需判断分子是否为0.

```java
public boolean isBoomerang(int[][] points) {
        int x1 = points[0][0];
        int x2 = points[1][0];
        int x3 = points[2][0];
        int y1 = points[0][1];
        int y2 = points[1][1];
        int y3 = points[2][1];
        return x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 -y2) != 0;
    }
```
