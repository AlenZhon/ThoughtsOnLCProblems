# 1252. Cells with Odd Values in a Matrix

## 题目

给定n和m表示一个 `n * m` 的零矩阵。给定`indices`数组，其中`indices[i] = [ri, ci]`。每次操作，都对矩阵的第`ri`行和第`ci`列的每个元素自增1。问经过所有操作，矩阵中的元素的奇数个数是多少。

>Given n and m which are the dimensions of a matrix initialized by zeros and given an array indices where `indices[i] = [ri, ci]`. For each pair of `[ri, ci]` you have to increment all cells in row ri and column ci by 1.
>
>Return the number of cells with odd values in the matrix after applying the increment to all indices.
>
>**Example 1:**
>
>>Input: n = 2, m = 3, indices = [[0,1],[1,1]]  
>>Output: 6  
>>Explanation: Initial matrix = [[0,0,0],[0,0,0]].  
>>After applying first increment it becomes [[1,2,1],[0,1,0]].  
>>The final matrix will be [[1,3,1],[1,3,1]] which contains 6 odd numbers.
>
>**Example 2:**
>
>>Input: n = 2, m = 2, indices = [[1,1],[0,0]]  
>>Output: 0  
>>Explanation: Final matrix = [[2,2],[2,2]].  
>>There is no odd number in the final matrix.
>
>**Constraints:**
>
> - 1 <= n <= 50
> - 1 <= m <= 50
> - 1 <= indices.length <= 100
> - 0 <= indices[i][0] < n
> - 0 <= indices[i][1] < m

## 解法

粗暴的Straight-forward。

时间复杂度`O(k * (m + n) + m*n)`，其中k是indices数组的长度。空间复杂度`O(m*n)`。

```java
public int oddCells(int n, int m, int[][] indices) {
        int[][] mat = new int[n][m];
        for (int[] index : indices) {
            for (int j = 0; j < m; j++) mat[index[0]][j]++;
            for (int i = 0; i < n; i++) mat[i][index[1]]++;
        }
        int count = 0;
        for (int i = 0; i< n; i++)
            for (int j = 0; j< m; j++)
                if ((mat[i][j] & 1) == 1) count++;
        return count;
    }
```

可以不初始化矩阵，只是初始化int[n]和int[m]数组用于存放每行和每列的增加次数。然后用奇偶数的乘法算出结果。

```java
public int oddCells(int m, int n, int[][] indices) {
        int[] rows = new int[m];
        int[] cols = new int[n];

        for (int[] index: indices) {
            rows[index[0]]++;
            cols[index[1]]++;
        }

        int oddR = 0, evenR = 0;
        int oddC = 0, evenC = 0;

        for (int i = 0; i < rows.length; i++) {
            if (rows[i] % 2 == 0) {
                evenR++;
            } else {
                oddR++;
            }
        }

        for (int i = 0; i < cols.length; i++) {
            if (cols[i] % 2 == 0) {
                evenC++;
            } else {
                oddC++;
            }
        }

        return evenR * oddC + evenC * oddR;
}
```
