# 1128. Number of Equivalent Domino Pairs

## 题目

>Given a list of `dominoes`, `dominoes[i] = [a, b]` is equivalent to `dominoes[j] = [c, d]` if and only if either (`a==c` and `b==d`), or (`a==d` and `b==c`) - that is, one domino can be rotated to be equal to another domino.
>
Return the number of pairs `(i, j)` for which `0 <= i < j < dominoes.length`, and `dominoes[i]` is equivalent to `dominoes[j]`.
>
>**Example 1:**
>
>>Input: dominoes = [[1,2],[2,1],[3,4],[5,6]]  
>>Output: 1
>
>**Constraints:**
>
> - 1 <= dominoes.length <= 40000
> - 1 <= dominoes[i][j] <= 9

## 解法

构造一个`int[9][9] a`用来保存domino的出现次数。我的写法。(2ms)

```java
public int numEquivDominoPairs(int[][] dominoes) {
        int[][] a = new int[9][9]; //[0 -- 8]
        for (int[] domino : dominoes){
            int i = domino[0], j = domino[1];
            if (i > j) {
                int temp = i; i = j; j = temp;
            }
            a[i - 1][j - 1]++;
        }
        int count = 0;
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                if (a[i][j] > 1)
                    count += a[i][j] * (a[i][j] - 1) / 2;
        return count;
    }
```

(1ms)

```java
public int numEquivDominoPairs(int[][] dominoes) {
        int[][] a = new int[9][9]; //[0 -- 8]
        for (int[] domino : dominoes){
            int i = domino[0], j = domino[1];
            a[i - 1][j - 1]++;
        }
        int count = 0;
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++){
                int sum = a[i][j];
                if (i != j) sum += a[j][i];
                if (sum > 1) count += sum * (sum - 1) / 2;
                a[i][j] = 0;
                a[j][i] = 0;
            }
        return count;
    }
```
