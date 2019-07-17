# 70 Climbing Stairs

## 题目描述

给定一正整数n为需要爬的台阶数，你可以一次选择上1级台阶或2级台阶，问总共有多少种不同的上台阶方法？  

You are climbing a stair case. It takes n steps to reach to the top.  
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

## 怎么解的

思考可以得到递推公式：  
（n>2）时，上n级台阶的方法 = 上n-1级台阶的方法（再多跨一级）+上n-2级台阶的方法。

斐波那契数列嘛。

一开始用了暴力递归O(2^n)，果然报Time Limits Exceeded。

```java
if (n==1) {return 1;}
else if (n==2) {return 2;}
else return climbStairs(n-1)+climbStairs(n-2);
```

转而用动态规划，自下而上迭代得出结果。由于不需要保留之前的数列元素，故使用两个变量存储。时间复杂度O(n)，空间复杂度O(1)。

```java
 public int climbStairs(int n) {
        int first = 1, second = 1;
        while (n >1) {
            int temp = first + second;
            second = first;
            first = temp;
            n--;
        }
        return first;
    }
```

## Notes

- 斐波那契数列的第45项已经大于Integer.MAX_VALUE。  
- 在Solution中有两种时间复杂度为O(logn)的解法，分别为矩阵运算和斐波那契数列的通项公式。代码贴在下面。

```java
 public class Solution {
    public int climbStairs(int n) {
        int[][] q = {{1, 1}, {1, 0}};
        int[][] res = pow(q, n);
        return res[0][0];
    }
    public int[][] pow(int[][] a, int n) {
        int[][] ret = {{1, 0}, {0, 1}};
        while (n > 0) {
            if ((n & 1) == 1) {
                ret = multiply(ret, a);
            }
            n >>= 1;
            a = multiply(a, a);
        }
        return ret;
    }
    public int[][] multiply(int[][] a, int[][] b) {
        int[][] c = new int[2][2];
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++) {
                c[i][j] = a[i][0] * b[0][j] + a[i][1] * b[1][j];
            }
        }
        return c;
    }
}
```

```java
public class Solution {
    public int climbStairs(int n) {
        double sqrt5=Math.sqrt(5);
        double fibn=Math.pow((1+sqrt5)/2,n+1)-Math.pow((1-sqrt5)/2,n+1);
        return (int)(fibn/sqrt5);
    }
}
```
