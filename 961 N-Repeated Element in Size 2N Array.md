# 961. N-Repeated Element in Size 2N Array

## 题目

一个数组里有2N个数，其中只有N+1个互不相同的数，有N个数是相同的。返回这个重复了N次的数。

>In a array A of size 2N, there are N+1 unique elements, and exactly one of these elements is repeated N times.
>
>Return the element repeated N times.
>
>**Example 1:**
>
>>Input: [1,2,3,3]  
>>Output: 3
>
>**Example 2:**
>
>>Input: [2,1,2,5,3,2]  
>>Output: 2  
>
>**Example 3:**
>
>>Input: [5,1,5,2,5,3,5,4]  
>>Output: 5
>
>**Note:**
>
> - 4 <= A.length <= 10000
> - 0 <= A[i] < 10000
> - A.length is even

## 解法

维护一个HashSet，如果`(!set.add(A[i]))`则说明A[i]重复了。

```java
public int repeatedNTimes(int[] A) {
        HashSet set = new HashSet<>();
        for (int i : A)
            if (!set.add(i)) return i;
        return -1;
    }
```

时间复杂度O(n)，空间复杂度O(n)。

是否可以找到不使用额外空间的方法？

考虑一个最简单的int[4]，其中有两个数相同设为 x 。那么这两个 x 的最大距离为3(此时`A[0] == A[3] == x`)。向数组中每加入两个数，就必然有一个为 x，最大距离不会增加。拓展到2N的数组中，只需找到`A[i]`与A`[i-1],A[i-2], A[i-3]`的相等关系即可。时间复杂度O(n)，空间复杂度O(1).

```java
public int repeatedNTimes(int[] A) {
        for (int i = 2; i< A.length; i++){
            if (A[i] == A[i-1] || A[i] == A[i-2] || A[i] == A[i-3])
                return A[i];
        }
        return -1;
    }
```

还可以从两个 x 的最小距离考虑。当x集中在连续区间时，最小距离相等均为1，当x均匀分布（即在数列中全占奇数位或全占偶数位），最小距离也相等且均为2。特殊情况是当int[4], A[0] == A[3]时，最小距离和最大距离都是3。

```java
public int repeatedNTimes(int[] A) {
        for (int i = 2; i< A.length; i++){
            if (A[i] == A[i-1] || A[i] == A[i-2])
                return A[i];
        }
        return A[0]; //[1,2,3,1] or [1,1,2,3]
    }
```
