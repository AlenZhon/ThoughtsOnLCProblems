# 463. Island Perimeter

## 题目

用一个二值化的二维数组表示一张海岛的地图。1表示陆地，2表示海水。已知地图上的陆地全部相连（只有一个岛）且岛内没有水源，求整个小岛的外周长。

>You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water.
>
>Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).
>
>The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.
>
>**Example:**
>
>>Input:  
>>[[0,1,0,0],  
>>&nbsp;[1,1,1,0],  
>>&nbsp;[0,1,0,0],  
>>&nbsp;[1,1,0,0]]  
>>Output: 16

## 解法

只想到了O(n^2)的解法，遍历地图，判断每块陆地的上下左右4个地块中有几块是海水（或地图边界），也就是有几条海岛边界，加到周长中。

```java
public int islandPerimeter(int[][] grid) {
        int perimeter = 0;
        for (int i = 0 ; i< grid.length; i++)
            for (int j = 0; j< grid[0].length; j++){
                if (grid[i][j] == 0) continue;
                int up = (i ==0 || grid[i-1][j] == 0) ? 1: 0;
                int down = (i == grid.length - 1 || grid[i+1][j] == 0) ? 1 : 0;
                int left = (j == 0 || grid[i][j-1] == 0) ? 1 : 0;
                int right = (j == grid[0].length - 1 || grid[i][j+1] == 0) ? 1: 0;
                perimeter += up + down + left + right;
            }
        return perimeter;
    }
```

还有一种方法是遍历地图，记录下陆地的块数`island`和陆地中相邻的个数`neighbour`（如题给例子，`island = 7, neighbour = 6`）。由于两块陆地如果相连，则总周长-2 （`2 * 4 -2 = 6`），所以最后只需返回`4 * island - 2 * neighbour`。

```java
public int islandPerimeter(int[][] grid) {
        int islands = 0, neighbours = 0;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    islands++; // count islands
                    if (i < grid.length - 1 && grid[i + 1][j] == 1) neighbours++; // count down neighbours
                    if (j < grid[i].length - 1 && grid[i][j + 1] == 1) neighbours++; // count right neighbours
                }
            }
        }

        return islands * 4 - neighbours * 2;
    }
```
