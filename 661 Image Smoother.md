# 661. Image Smoother

## 题目

一个数值范围在`[0, 255]`的矩阵，对每个元素，加上它周围的所有元素再做平均，将平均值取为新值。返回经过这样处理后的矩阵。

>Given a 2D integer matrix `M` representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.
>
>Example 1:
>
>>Input:  
>>[[1,1,1],  
>>[1,0,1],  
>>[1,1,1]]  
>>Output:  
>>[[0, 0, 0],  
>>[0, 0, 0],  
>>[0, 0, 0]]  
>>Explanation:  
>>For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0  
>>For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0  
>>For the point (1,1): floor(8/9) = floor(0.88888889) = 0
>
>**Note:**
>
> - The value in the given matrix is in the range of [0, 255].
> - The length and width of the given matrix are in the range of [1, 150].

## 解法

水题。注意一下矩阵边界的元素即可。  
在OJ上把取平均的`subi subj`循环写成函数，能显著降低运行时间（？）

```java
public int[][] imageSmoother(int[][] M) {
        int len = M.length, wid = M[0].length;
        int[][] ret = new int[len][wid];
        for (int i = 0; i< len; i++)
            for (int j = 0; j< wid; j++)
                ret[i][j] = smoother(M, i, j);
        return ret;
    }
    private int smoother(int[][] matrix, int i, int j) {
        int count = 0, row = matrix.length, col = matrix[0].length, sum =0;
        for (int subi = i - 1; subi <= i + 1; subi++)
            for (int subj = j - 1; subj <= j+1; subj++) {
                if (subi < 0 || subi >= row || subj < 0 || subj >= col) continue;
                count++;
                sum += matrix[subi][subj];
            }
        return sum / count;
    }
```
