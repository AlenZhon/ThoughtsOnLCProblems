# 942. DI String Match

## 题目

给定一个字符串，里面的字符只有两种可能"I"或者"D"，分别代表increase增加和decrease减少。字符串长度为 N，根据字符串生成一个包含着[0, 1, ..., N]所有整数的数组，满足：  
当字符串中S[i] = "I"时， A[i] < A[i+1];  
当字符转中S[i] = "D"时， A[i] > A[i+1];

>Given a string S that **only** contains "I" (increase) or "D" (decrease), let N = S.length.
>
>Return **any** permutation A of [0, 1, ..., N] such that for all i = 0, ..., N-1:
>
> - If `S[i] == "I"`, then `A[i] < A[i+1]`
> - If `S[i] == "D"`, then `A[i] > A[i+1]`
>
>**Example 1:**
>
>>Input: "IDID"  
>>Output: [0,4,1,3,2]
>
>**Example 2:**
>
>>Input: "III"  
>>Output: [0,1,2,3]
>
>Example 3:
>
>>Input: "DDI"  
>>Output: [3,2,0,1]
>
>Note:
>
> - 1 <= S.length <= 10000
> - S only contains characters "I" or "D".

## 解法

用两个指针分别指向[0, N]中还没被使用过的最小和最大整数。如果此时是"I"，将最小整数加入数组，反之则将最大整数加入数组。

时间复杂度O(N), 空间复杂度O(N)（不用toCharArray()的话可以说O(1)吗）

```java
public int[] diStringMatch(String S) {
        char[] c = S.toCharArray();
        int N = c.length, i = 0, j = N;
        int[] ret = new int[N + 1];
        for (int k = 0; k < N; k++){
            if (c[k] == 'I')
                ret[k] = i++;
            else if (c[k] == 'D')
                ret[k] = j--;
        }
        ret[N] = i;
        return ret;
    }
```
