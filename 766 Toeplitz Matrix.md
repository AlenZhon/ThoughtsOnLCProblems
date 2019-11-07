# 766. Toeplitz Matrix

## 题目

判断一个2D数列能否构成Toeplitz Matrix，即矩阵中同一条对角线（从左上到右下）上的元素都相等。

>A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same element.
>
>Now given an M x N matrix, return True if and only if the matrix is Toeplitz.
>
>Example 1:
>
>>Input:  
>>matrix = [  
>>`[1,2,3,4]`,  
>>`[5,1,2,3]`,  
>>`[9,5,1,2]`  
>>]  
>>Output: True  
>>Explanation:
>>In the above grid, the diagonals are:
>>`"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]"`.  
>>In each diagonal all elements are the same, so the answer is `True`.
>
>Example 2:
>
>>Input:  
>>matrix = [
>>`[1,2],`  
>>`[2,2]`  
>>]
>>Output: False  
>>Explanation:  
>>The diagonal `"[1, 2]"` has different elements.
>
>Note:
>
> - `matrix` will be a 2D array of integers.
> - `matrix` will have a number of rows and columns in range `[1, 20]`.
> - `matrix[i][j]` will be integers in range `[0, 99]`.
>
>Follow up:
>
> - What if the matrix is stored on disk, and the memory is limited such that you can only load at most one row of the matrix into the memory at once?
> - What if the matrix is so large that you can only load up a partial row into the memory at once?

## 解法

顶多了20行20列，暴力破解直接比。时间复杂度O(m*n)，空间O(1)

```java
public boolean isToeplitzMatrix(int[][] matrix) {
        int rows= matrix.length, cols = matrix[0].length;
        for (int c = 0; c < cols; c++)
            for (int i = 0; i< rows && c + i < cols; i++)
                if (matrix[i][c + i] != matrix[0][c]) return false;

        for (int r = 0; r < rows; r++)
            for (int j = 0; j < cols && r + j < rows; j++)
                if (matrix[r + j][j] != matrix[r][0]) return false;

        return true;
    }
```

用r和c表示当前的元素下标，那么在矩阵的范围内，可直接比较`matrix[r][c]`和`matrix[r-1][c-1]`。因此可以把上面的两个循环写成一个：

```java
public boolean isToeplitzMatrix(int[][] matrix){
      int rows = matrix.length, cols = matrix[0].length;
      for (int r = 0; r < rows; r++)
          for (int c = 0; c < cols; c++)
              if (r > 0 && c > 0 && matrix[r-1][c-1] != matrix[r][c])
                  return false;
      return true;
}
```

## 另一种解法

两个元素`matrix[r1][c1]`和`matrix[r2][c2]`在同一条对角线上， 当且仅当 `r1 - c1 == r2 - c2`。

因此我们可以构造HashMap，key 为 `r-c`, value为`matrix[r][c]`。

```java
public boolean isToeplitzMatrix(int[][] matrix) {
        Map<Integer, Integer> groups = new HashMap();
        for (int r = 0; r < matrix.length; ++r) {
            for (int c = 0; c < matrix[0].length; ++c) {
                if (!groups.containsKey(r-c))
                    groups.put(r-c, matrix[r][c]);
                else if (groups.get(r-c) != matrix[r][c])
                    return False;
            }
        }
        return True;
    }
```

时间复杂度仍为O(m * n), 空间复杂度O(m + n)。

对于Follow-up的第一个问题可以用这种解法去解决。对每一行中的元素，比较它和hashMap里对应的value是否相等。

对于第二个问题， 评论区的老哥说需要在这个解法上使用Loop nest Optimation并丢出来了一个[wiki链接](https://en.wikipedia.org/wiki/Loop_nest_optimization)。看起来是一个将较大的矩阵分块以降低运算时间的方法。
