# 733. Flood Fill

## 题目

用一个二维数组表示一张图片，数组中的元素为一个像素，范围在[0,65535]，每个整数表示一种不同的颜色。现在需要实现颜色填充的功能：给定一个起始像素和一个颜色`newColor`，将起始像素和所有和起始像素同一个色块的像素填充成`newColor`。

>An `image` is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).
>
>Given a coordinate (sr, sc) representing the starting pixel (row and column) of the flood fill, and a pixel value newColor, "flood fill" the image.
>
>To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.
>
>At the end, return the modified image.
>
>**Example 1:**
>
>>Input:  
>>image = `[[1,1,1],[1,1,0],[1,0,1]]`  
>>sr = 1, sc = 1, newColor = 2
>>Output: `[[2,2,2],[2,2,0],[2,0,1]]`  
>>Explanation:  
>>From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
>
>**Note:**
>
> - The length of image and image[0] will be in the range `[1, 50]`.
> - The given starting pixel will satisfy `0 <= sr < image.length` and `0 <= sc < image[0].length`.
> - The value of each color in image[i][j] and newColor will be an integer in `[0, 65535]`.

## 解法

首先想到的是递归，看了hint也是这么说的。所以就暴力撸了一个。第一次提交的时候没有判断 “起始像素就是newColor这个颜色”的情况，报了StackOverFlow。时间复杂度和空间复杂度都是O(N)， N是像素的个数（最坏情况下要把所有的像素都遍历过）。

```java
public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if (image[sr][sc] != newColor)
            helper(image, sr, sc, image[sr][sc], newColor);
        return image;
    }

    private void helper(int[][] a, int i, int j, int oriColor, int newColor) {
        if (a[i][j] == oriColor) a[i][j] = newColor;
        if (i-1 >= 0 && a[i-1][j] == oriColor)
            helper(a, i-1, j, oriColor, newColor);
        if (j-1 >= 0 && a[i][j-1] == oriColor)
            helper(a, i, j-1, oriColor, newColor);
        if (i+1 <= a.length - 1 && a[i+1][j] == oriColor)
            helper(a, i+1, j, oriColor, newColor);
        if (j+1 <= a[0].length - 1 && a[i][j+1] == oriColor)
            helper(a, i, j+1, oriColor, newColor);
        return;
    }
```

这里的判断条件一开始写成这样，主要是想 如果周围像素本来就不是oriColor，就可以少递归一次。写得好看一些的话：

```java
public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int or = image[sr][sc];
        if(newColor == or)
            return image;
        dfs(image, sr, sc, or, newColor);
        return image;
    }

    public void dfs(int[][] image, int i, int j, int or, int nc){
        if(i < 0 || i >= image.length || j < 0 || j >= image[0].length || image[i][j] != or)
            return;
        image[i][j] = nc;
        dfs(image,i-1,j,or,nc);
        dfs(image,i+1,j,or,nc);
        dfs(image,i,j-1,or,nc);
        dfs(image,i,j+1,or,nc);
    }
```
