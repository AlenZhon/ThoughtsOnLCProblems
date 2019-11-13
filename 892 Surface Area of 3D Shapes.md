# 892. Surface Area of 3D Shapes

## 题目

在`N*N`的网格上我们摆放一些正方体。给定一个`grid[][]`数组，`grid[i][j]`表示在`(i,j)`网格上竖直垒着`grid[i][i]`块 `1*1*1` 的正方体。所以整个数组表示了在空间中一堆正方体的摆放情况。求这堆正方体的表面积之和。

>On a `N * N` grid, we place some `1 * 1 * 1` cubes.
>
>Each value v = grid[i][j] represents a tower of v cubes placed on top of grid cell (i, j).
>
>Return the total surface area of the resulting shapes.
>
>**Example 1:**
>
>>Input: [[2]]  
>>Output: 10
>
>**Example 2:**
>
>>Input: [[1,2],[3,4]]  
>>Output: 34
>
>**Example 3:**
>
>>Input: [[1,0],[0,2]]  
>>Output: 16
>
>**Example 4:**
>
>>Input: [[1,1,1],[1,0,1],[1,1,1]]  
>>Output: 32
>
>**Example 5:**
>
>>Input: [[2,2,2],[2,1,2],[2,2,2]]
>>Output: 46
>
>Note:
>
> - `1 <= N <= 50`
> - `0 <= grid[i][j] <= 50`

## 解法

和 *883 Projection Area of 3D shape* 的题目背景相同。一开始我认为三视图的面积和都求出来了，乘个2不就完事了。结果发现示例4和示例5特意提示了存在凹面的情况。

考虑一个网格上的方块。它的上下面是不会被挡住的，而如果它的前后左右四个方向中哪一面比它高，那么它的那一面就会被合并，不算在表面积中。同时如果这个网格是边界网格，它对应边界的那个面全都算在内。

所以我们遍历矩阵，对每个网格上的方块进行计算。时间复杂度O(N * N)， 空间O(1)。

```java
public int surfaceArea(int[][] grid) {
        int sum = 0, N = grid.length;
        for (int i = 0; i< N; i++){
            for (int j = 0; j< N; j++) {
                if (grid[i][j] == 0) continue;
                sum += 2;
                sum += Math.max(grid[i][j] - (i > 0 ? grid[i - 1][j] : 0), 0);
                sum += Math.max(grid[i][j] - (i < N - 1 ? grid[i + 1][j] : 0), 0);
                sum += Math.max(grid[i][j] - (j > 0 ? grid[i][j - 1] : 0), 0);
                sum += Math.max(grid[i][j] - (j < N - 1 ? grid[i][j + 1] : 0), 0);
            }
        }
        return sum;
    }
```

或者这样写：

```java
public int surfaceArea(int[][] grid) {
        int res = 0;
        if(grid == null || grid.length == 0)return res;
        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid.length; j++){
                if (grid[i][j]!=0) res+=2;
                if(i == 0) res+= grid[i][j];
                if(j == 0) res+= grid[i][j];
                if(i == grid.length-1) res+= grid[i][j];
                if(j == grid.length-1) res+= grid[i][j];
                if(i != 0) res+= Math.abs(grid[i][j]-grid[i-1][j]);
                if(j!=0) res += Math.abs(grid[i][j]-grid[i][j-1]);
            }
        }
        return res;
    }
```
