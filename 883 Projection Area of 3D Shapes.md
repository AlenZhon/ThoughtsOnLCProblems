# 883. Projection Area of 3D Shapes

## 题目

在`N*N`的网格上我们摆放一些正方体。给定一个`grid[][]`数组，`grid[i][j]`表示在`(i,j)`网格上竖直垒着`grid[i][i]`块 `1*1*1` 的正方体。所以整个数组表示了在空间中一堆正方体的摆放情况。求这堆正方体的三视图（从上方，前方和侧面）面积之和。

>On a `N * N` grid, we place some `1 * 1 * 1` cubes that are axis-aligned with the x, y, and z axes.
>
>Each value `v = grid[i][j]` represents a tower of `v` cubes placed on top of grid cell `(i, j)`.
>
>Now we view the projection of these cubes onto the `xy, yz, and zx` planes.
>
>A projection is like a shadow, that maps our 3 dimensional figure to a 2 dimensional plane.
>
>Here, we are viewing the "shadow" when looking at the cubes from the top, the front, and the side.
>
>Return the total area of all three projections.
>
>**Example 1:**
>
>>Input: [[2]]  
>>Output: 5  
>
>**Example 2:**
>
>>Input: [[1,2],[3,4]]  
>>Output: 17  
>>Explanation:  
>>Here are the three projections ("shadows") of the shape made with each axis-aligned plane.
>
>**Example 3:**
>
>>Input: [[1,0],[0,2]]  
>>Output: 8  
>
>**Example 4:**  
>
>>Input: [[1,1,1],[1,0,1],[1,1,1]]  
>>Output: 14  
>
>**Example 5:**
>
>>Input: [[2,2,2],[2,1,2],[2,2,2]]  
>>Output: 21  
>
>Note:
>
> - 1 <= grid.length = grid[0].length <= 50
> - 0 <= grid[i][j] <= 50

## 解法

读懂了题目就很好做了。就是求底面积、前面积和侧面积。底面积就是矩阵非0元素的个数。前面积和侧面积分别为按行和按列的矩阵元素最大值之和。

尤其是Note里明确规定`grid[][]`形成的矩阵是方阵，就可以把前面积和侧面积放到同一个二层循环里求。时间复杂度O(grid.length ^ 2)，空间复杂度O(1)。

```java
public int projectionArea(int[][] grid) {
        int sum = 0;
        for (int i = 0; i< grid.length; i++) {
            int rowMax = 0;
            int colMax = 0;
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] > 0) sum++;
                rowMax = grid[i][j] > rowMax ? grid[i][j] : rowMax;
                colMax = grid[j][i] > colMax ? grid[j][i] : colMax;
            }
            sum += rowMax + colMax;
        }
        return sum;
    }
```
