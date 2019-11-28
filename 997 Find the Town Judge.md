# 997. Find the Town Judge

## 题目

镇子里可能有一个铁面无私的镇法官。法官的要求是：  
1.法官不相信镇子里的任何人。  
2.镇子里除了法官的其他人都相信法官。
3.如果有，镇子里只能有一个镇法官。

现在给定镇子人数N，用二维数组表示一个相信列表，每一行中的[A,B]表示居民A相信居民B。找到镇法官是哪位，如果没有，返回-1。

>In a town, there are N people labelled from 1 to N.  There is a rumor that one of these people is secretly the town judge.
>
>If the town judge exists, then:
>
> - The town judge trusts nobody.
> - Everybody (except for the town judge) trusts the town judge.
> - There is exactly one person that satisfies properties 1 and 2.
>
>You are given trust, an array of pairs trust[i] = [a, b] representing that the person labelled a trusts the person labelled b.
>
>If the town judge exists and can be identified, return the label of the town judge.  Otherwise, return -1.
>
>**Example 1:**
>
>>Input: N = 2, trust = [[1,2]]  
>>Output: 2  
>
>**Example 2:**
>
>>Input: N = 3, trust = [[1,3],[2,3]]  
>>Output: 3
>
>**Example 3:**
>
>>Input: N = 3, trust = [[1,3],[2,3],[3,1]]  
>>Output: -1
>
>**Example 4:**
>
>>Input: N = 3, trust = [[1,2],[2,3]]  
>>Output: -1
>
>**Example 5:**
>
>>Input: N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]  
>>Output: 3  
>
>**Note:**
>
> - `1 <= N <= 1000`
> - `trust.length <= 10000`
> - `trust[i] are all different`
> - `trust[i][0] != trust[i][1]`
> - `1 <= trust[i][0], trust[i][1] <= N`

## 解法

根据题意，如果镇法官存在，那么TA不相信任何人，且其他任何人都相信TA。构造一个数组存储居民有没有相信的人，找到元素为0 的数组下标，即这个家伙不相信任何人。这就是镇法官的候选人。如果这个候选人出现在trust[][1]的次数达到了N-1次，表示其他所有人都相信他。

```java
public int findJudge(int N, int[][] trust) {
        int[] a = new int[N]; // [0, N - 1]
        for (int i = 0; i< trust.length; i++)
            a[trust[i][0] - 1] = 1;
        int candidate = -1;
        for (int i = 0; i< a.length; i++)
            if (a[i] == 0) candidate = i;
        if (candidate == -1) return -1;  // no town judge that trust nobody
        int count = 0;
        for (int i = 0; i< trust.length; i++)
            if (trust[i][1] == candidate + 1) count++; //everyone (except candidate)
        if (count == N - 1) return candidate + 1;
        else return -1;
    }
```

时间复杂度O(N)，空间复杂度O(N)。
