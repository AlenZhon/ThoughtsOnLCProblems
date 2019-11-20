# 944. Delete Columns to Make Sorted

## 题目

一个`String[]`，其中每个字符串的长度均相同，相当于构成了一个字符组成的二维矩阵。删去矩阵的某些列使得剩下的每一列都按照字符**非降序**排列，问最少需要删去多少列。

>We are given an array A of N lowercase letter strings, all of the same length.
>
>Now, we may choose any set of deletion indices, and for each string, we delete all the characters in those indices.
>
>For example, if we have an array `A = ["abcdef","uvwxyz"]` and deletion indices {0, 2, 3}, then the final array after deletions is `["bef", "vyz"]`, and the remaining columns of A are `["b","v"], ["e","y"], and ["f","z"]`.  (Formally, the c-th column is `[A[0][c], A[1][c], ..., A[A.length-1][c]]`.)
>
>Suppose we chose a set of deletion indices D such that after deletions, each remaining column in A is in **non-decreasing** sorted order.
>
>Return the minimum possible value of D.length.
>
>**Example 1:**
>
>>Input: ["cba","daf","ghi"]  
>>Output: 1  
>>Explanation:  
>>After choosing D = {1}, each column ["c","d","g"] and ["a","f","i"] are in non-decreasing sorted order.  
>>If we chose D = {}, then a column ["b","a","h"] would not be in non-decreasing sorted order.
>
>**Example 2:**
>
>>Input: ["a","b"]  
>>Output: 0  
>>Explanation: D = {}
>
>**Example 3:**
>
>>Input: ["zyx","wvu","tsr"]  
>>Output: 3  
>>Explanation: D = {0, 1, 2}
>
>**Note:**
>
> - 1 <= A.length <= 100
> - 1 <= A[i].length <= 1000

## 解法

没有啥想法，搞成char[][]直接二重循环做？

时间复杂度`O(m * n)`，空间复杂度`O(m * n)`。

```java
public int minDeletionSize(String[] A) {
        char[][] c = new char[A.length][A[0].length()];
        for (int i = 0; i< A.length; i++)
            c[i] = A[i].toCharArray();
        int count = 0;
        for (int j = 0; j < c[0].length; j++)
            for (int i = 1; i< c.length; i++)
                if (c[i][j] < c[i-1][j]) {
                    count++;
                    break;
                }
        return count;
    }
```

1ms的代码样例用的charAt()，不过将比较的部分写成了子函数。

```java
public int minDeletionSize(String[] a) {
        int result = 0;
        int stringLength = a[0].length();

        for (int i = 0; i < stringLength; i++) {
            if (isNotSort(a, i)) {
                result++;
            }
        }
        return result;
    }

    public static boolean isNotSort(String[] s, int num) {
        char prev = s[0].charAt(num);
        for (String value : s) {
            char curr = value.charAt(num);
            if (curr < prev)
                return true;
            prev = curr;
        }
        return false;
    }
```
