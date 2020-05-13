# 62. Unique Paths

## 题目

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

## 解法

### 排列组合问题

由于只有向右和向下两种方向，实际上最后的答案容易得到是`C^{m-1}_{m+n-2}`

### 经典动态规划
dp[][] 第一行和第一列都是1，状态转移即可。时间和空间复杂度O(m*n)

```java
public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int i =0; i< m; ++i){
            for (int j = 0; j<n; ++j){
                if (i == 0 || j== 0) {
                    dp[i][j] = 1;
                } else {
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }
```

### 空间上的优化

上面我们可以发现，状态的转移实际上只涉及上一行和这一行的数据。我们可以将空间复杂度减小为O(2n).用pre存上一行的数据那么状态转移方程里的`dp[i-1][j]`变成`pre[j]`。

```java
public int uniquePaths(int m, int n) {
        int[] pre = new int[n];
        int[] cur = new int[n];
        for (int i = 0; i < n ;i++) pre[i] = 1;
        for (int i = 0; i < n ;i++) cur[i] = 1;
        for (int i = 1; i < m;i++){
            for (int j = 1; j < n; j++){
                cur[j] = cur[j-1] + pre[j];
            }
            pre = cur.clone();
        }
        return pre[n-1]; 
    }
```

进一步，在状态转移之前pre[j]里就存着cur[j]的值。所以只需一个数组，空间复杂度减小为O(n).

```java
public int uniquePaths(int m, int n) {       
        int[] cur = new int[n];
        for (int i = 0; i< n; i++) cur[i] = 1;
        for (int i = 1; i< m; i++){
            for (int j = 1; j< n; j++){
                cur[j] += cur[j-1];
            }
        }
        return cur[n-1];
    }
```




