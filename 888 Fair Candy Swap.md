# 888. Fair Candy Swap

## 题目

Alice 和 Bob 手上分别有一些糖果棒，每块糖果的长度可能不相同。现在两人分别拿出一块糖果进行交换，交换之后两人糖果的总长度相等了。给定两人手上每块糖果的长度，找到交换方案。（交换方案保证存在，如果有多个方案输出一个即可。）

>Alice and Bob have candy bars of different sizes: `A[i]` is the size of the `i-th` bar of candy that Alice has, and `B[j]` is the size of the `j-th` bar of candy that Bob has.
>
>Since they are friends, they would like to exchange one candy bar each so that after the exchange, they both have the same total amount of candy.  (The total amount of candy a person has is the sum of the sizes of candy bars they have.)
>
>Return an integer array ans where `ans[0]` is the size of the candy bar that Alice must exchange, and `ans[1]` is the size of the candy bar that Bob must exchange.
>
>If there are multiple answers, you may return any one of them.  It is guaranteed an answer exists.
>
>**Example 1:**
>
>>Input: A = [1,1], B = [2,2]  
>>Output: [1,2]  
>
>**Example 2:**
>
>>Input: A = [1,2], B = [2,3]  
>>Output: [1,2]  
>
>**Example 3:**
>
>>Input: A = [2], B = [1,3]  
>>Output: [2,3]  
>
>**Example 4:**
>
>>Input: A = [1,2,5], B = [2,4]  
>>Output: [5,4]
>
>**Note:**
>
> - `1 <= A.length <= 10000`
> - `1 <= B.length <= 10000`
> - `1 <= A[i] <= 100000`
> - `1 <= B[i] <= 100000`
> - It is guaranteed that Alice and Bob have different total amounts of candy.
> - It is guaranteed there exists an answer.

## 解法

设初始时刻两人糖果的总长度为`sa, sb`，最后两人拿出来交换的糖果长度为`x, y`。肯定有：

`sa - x + y = sb - y + x`

等价于： `y = (sb - sa) / 2 + x`。 只需判断y在不在B数组里即可。时间复杂度`O(len(A) + len(B))`，提前把B的所有元素存入HashSet，空间复杂度`O(len(B))`。

```java
public int[] fairCandySwap(int[] A, int[] B) {
        int sumA = 0, sumB = 0;
        HashSet<Integer> set = new HashSet<>();
        for (int ai : A) sumA += ai;
        for (int bi : B) {sumB += bi; set.add(bi);}
        int add = (sumB - sumA) / 2;

        for (int ai : A)
            if (set.contains(ai + add))
                return new int[]{ai, ai + add};
        return new int[2];
    }
```

更快的方法是把Set用一个`boolean[1000001]`代替。
