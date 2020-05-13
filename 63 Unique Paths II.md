# 63. Unique Paths II

## 题目

>一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。
>
>机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。
>
>现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？
>
>网格中的障碍物和空位置分别用 1 和 0 来表示。
>
>**说明：** m 和 n 的值均不超过 100。
>
>**示例 1:**
>
>**输入:**
>>[  
>>  [0,0,0],  
>>  [0,1,0],  
>>  [0,0,0]  
>>]  
>>**输出:** 2  
>**解释:**  
>>3x3 网格的正中间有一个障碍物。  
>>从左上角到右下角一共有 2 条不同的路径：
>> 1. 向右 -> 向右 -> 向下 -> 向下
>> 2. 向下 -> 向下 -> 向右 -> 向右

## 解法

就在状态转移方程里加一个对于obstacle数组对应位置的判断。

自己写的繁琐了不是很优雅。以为题意隐含起点和终点都不能有障碍物所以一开始没有提前判断。
```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        if (obstacleGrid[0][0] == 1 || obstacleGrid[m-1][n-1] == 1) return 0;
        for (int i = 0; i< m; i++){
            for (int j =0; j< n; j++){
                if (i==0){
                    if (j==0) {dp[i][j] = 1; continue;}
                    dp[0][j] = (obstacleGrid[0][j] == 1) ? 0: dp[0][j-1];
                }else if (j == 0){
                    dp[i][0] = (obstacleGrid[i][0] == 1) ? 0: dp[i-1][0];
                }else {
                    dp[i][j] = (obstacleGrid[i-1][j] == 1 ? 0 : dp[i-1][j]) 
                                + (obstacleGrid[i][j-1] == 1 ? 0 : dp[i][j-1]); 
                }
            }
        }
        return dp[m-1][n-1];
    }
```

思考了一下，初始的时候如果第一行/列某个位置有障碍物，那么这个位置及其以后的dp[][]必须是0.

修改写法成如下形式:
```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        if (obstacleGrid[m-1][n-1] == 1) return 0;
        for (int i = 0; i< m; i++){
            if (obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++){
            if (obstacleGrid[0][j] == 1) break;
            dp[0][j] = 1;
        }
        for (int i =1 ; i< m; i++){
            for (int j = 1; j< n; j++){
                if (obstacleGrid[i][j] == 1) continue;
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
```

### 空间上的优化

同样可以优化成一行。

```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[] dp = new int[n];
        if (obstacleGrid[0][0] == 1 || obstacleGrid[m-1][n-1] == 1) return 0;

        for (int j = 0; j < n; j++){
            if (obstacleGrid[0][j] == 1) break;
            dp[j] = 1;
        }
        for (int i = 1; i< m; i++){
            if (obstacleGrid[i][0] == 1) dp[0] = 0;
            for (int j = 1; j< n; j++){
                dp[j] = (obstacleGrid[i][j] == 1) ? 0: dp[j] + dp[j-1];
            }
        }
        return dp[n-1];
    }
```
