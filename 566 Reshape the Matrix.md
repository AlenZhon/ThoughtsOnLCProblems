# 566. Reshape the Matrix

## 题目

实现Matlab中的reshape函数。即给定一个矩阵（二维的）和新矩阵的行数`r`和列数`c`，将原矩阵按照行优先的顺序转化成`r*c`的新矩阵。如果行数和列数不合法，则返回原矩阵。

>You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.
>
>The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.
>
>If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.
>
>**Example 1:**
>
>>Input:  
>>nums =  
>>`[[1,2], [3,4]]`  
>>r = 1, c = 4  
>>Output:  
>>`[[1,2,3,4]]`  
>>Explanation:
>>The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
>
>**Example 2:**
>
>>Input:  
>>nums =  
>>[[1,2], [3,4]]  
>>r = 2, c = 4  
>>Output:  
>>[[1,2],  
>> [3,4]]  
>>Explanation:
>>There is no way to reshape a `2 * 2` matrix to a `2 * 4` matrix. So output the original matrix.
>
>**Note:**
>
> - The height and width of the given matrix is in range [1, 100].
> - The given r and c are all positive.

## 解法

简单粗暴地一个个遍历呗。时间复杂度O(M*N)

```java
public int[][] matrixReshape(int[][] nums, int r, int c) {
        if (nums.length * nums[0].length != r * c) return nums;
        int[][] ret = new int[r][c];
        int rows = 0, cols = 0;
        for (int i=0; i< nums.length; i++)
            for (int j = 0; j< nums[0].length; j++) {
                ret[rows][cols++] = nums[i][j];
                if (cols == c){
                    rows++;
                    cols = 0;
                }
            }
        return ret;
    }
```

实际上，如果按照内存中数组的存储方式，我们可以知道二维数组在内存中就是按照行优先的顺序存储成一维的。那么，程序可以简化为：

```java
public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length)
            return nums;
        for (int i = 0; i < r * c; i++) {
           res[i / c][i % c] = nums[i / nums[0].length][i % nums[0].length];
        }
        return res;
    }
```
