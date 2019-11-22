# 985. Sum of Even Numbers After Queries

## 题目

给定一个初始数组A，同时给定操作数组`queries[][]`，对于数组的第i个元素表示一次对数组A的操作，具体表示为`A[queries[i][1]]+= queries[i][0]`。

以数组的形式返回每一次操作后数组A中为偶数的元素之和。

>We have an array A of integers, and an array queries of queries.
>
>For the i-th query `val = queries[i][0]`, `index = queries[i][1]`, we add `val` to `A[index]`.  Then, the answer to the i-th query is the sum of the even values of A.
>
>(Here, the given `index = queries[i][1]` is a **0-based index**, and each query permanently modifies the array A.)
>
>Return the answer to all queries.  Your answer array should have `answer[i]` as the answer to the i-th query.
>
>Example 1:
>
>>Input: A = `[1,2,3,4]`, queries = `[[1,0],[-3,1],[-4,0],[2,3]]`  
>>Output: `[8,6,2,4]`  
>>Explanation:  
>>At the beginning, the array is `[1,2,3,4]`.  
>>After adding 1 to A[0], the array is `[2,2,3,4]`, and the sum of even values is 2 + 2 + 4 = 8.  
>>After adding -3 to A[1], the array is `[2,-1,3,4]`, and the sum of even values is 2 + 4 = 6.  
>>After adding -4 to A[0], the array is `[-2,-1,3,4]`, and the sum of even values is -2 + 4 = 2.  
>>After adding 2 to A[3], the array is `[-2,-1,3,6]`, and the sum of even values is -2 + 6 = 4.  
>
>Note:
>
> - `1 <= A.length <= 10000`
> - `-10000 <= A[i] <= 10000`
> - `1 <= queries.length <= 10000`
> - `-10000 <= queries[i][0] <= 10000`
> - `0 <= queries[i][1] < A.length`

## 解法

如果用brute force，每一次操作重新算一次数组中的偶数之和`sum`，时间复杂度就变成了O(M * N)，M为Queries的长度，N为A的长度。

通过计算每次操作的`sum`的增量来降低时间复杂度。

首先把数组A初始时偶数之和算出来记为sum。假设`A[queries[i][1]]`为`curr`，`queries[i][0]`是`add`。

根据加法的奇偶关系，可以有四种情况：

- curr为偶数，add为偶数，则两者相加为偶数。sum中已经有了curr，只需 `sum+=add;`
- curr为偶数，add为奇数，则两者相加为奇数。需要在sum中减去curr。 `sum-=curr;`
- curr为奇数，add为偶数，两者相加为奇数，不改变sum的值。
- curr为奇数，add为偶数，两者相加为偶数，相当于 `sum+=curr+add;`

每次更新A[queries[i][1]]，并把计算的sum填入数组中。时间复杂度为O(M + N)，空间复杂度O(1)（因为返回的数组长度是必须要有的）。

```java
public int[] sumEvenAfterQueries(int[] A, int[][] queries) {
        int[] ret = new int[queries.length];
        int sum = 0;
        for (int a : A)
            if ((a & 1) == 0) sum+=a;

        for (int i = 0; i< queries.length; i++){
            int curr = A[queries[i][1]], add = queries[i][0];
            if ((curr & 1) == 0) {
                if ((add & 1) == 0) sum+=add;
                else sum -=curr;
            } else {
                if ((add & 1) == 1) sum+= curr + add;
            }
            ret[i] = sum;
            A[queries[i][1]] += add;
        }
        return ret;
    }
```
