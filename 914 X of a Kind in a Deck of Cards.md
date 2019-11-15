# 914. X of a Kind in a Deck of Cards

## 题目

现在有一堆牌，牌上的整数范围在`[1, 10000)`。问能不能得到一个`X (X>=2)`，使得这堆牌分成若干堆，每堆中有相同数字的X张牌。

>In a deck of cards, each card has an integer written on it.
>
>Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:
>
> - Each group has exactly X cards.
> - All the cards in each group have the same integer.
>
>**Example 1:**
>
>>Input: [1,2,3,4,4,3,2,1]  
>>Output: true  
>>Explanation: Possible partition [1,1],[2,2],[3,3],[4,4]
>
>**Example 2:**
>
>>Input: [1,1,1,2,2,2,3,3]  
>>Output: false  
>>Explanation: No possible partition.
>
>**Example 3:**
>
>>Input: [1]  
>>Output: false  
>>Explanation: No possible partition.
>
>**Example 4:**
>
>>Input: [1,1]  
>>Output: true  
>>Explanation: Possible partition [1,1]
>
>**Example 5:**
>
>>Input: [1,1,2,2,2,2]  
>>Output: true  
>>Explanation: Possible partition [1,1],[2,2],[2,2]
>
>**Note:**
>
> - 1 <= deck.length <= 10000
> - 0 <= deck[i] < 10000

## 解法

先把不同数字牌的出现次数存下来，再比较这些出现次数。

乍一看以为是找到最小出现次数，其他牌的出现次数都是它的整数倍。但实际上是要找到所有出现次数的最大公约数，如`[1,1,1,1,2,2,2,2,2,2]`

```java
public boolean hasGroupsSizeX(int[] deck) {
        int[] kind = new int[10000];
        for (int card :deck)
            kind[card]++;
        int gcd = 0;
        for (int i : kind){
            if (i == 0) continue;
            if (gcd == 0) gcd = i;
            else gcd = findGCD(gcd, i);
        }
        return gcd > 1;
    }

    private int findGCD(int a, int b){
        // definitely b is greater than a
        int temp = b % a;
        while (temp > 0) {
            b = a;
            a = temp;
            temp = b % a;
        }
        return a;
    }
```

关于时间复杂度的分析：

对于辗转相除法，如果算法要经过n步运算，则n次辗转相除后得到的便是最大公约数，n+1次为`u_(n+1) = 0`。将n+1次的余数组成一个数列，和斐波那契数列进行比较。

>`u_n = d >= 1 = F_0`
>`u_(n - 1) >= 1 = F_1`

数学归纳法可以证明 `u_(n -k) >= F_k`， 于是有`b = u_0 >= F_n, a = u_1 >= F_(n - 1)`。而求斐波那契数列有性质 `F_n > (1.618) ^ n / sqrt(5)` 所以运算次数的上限即确定为对数级。对于findGCD(a, b)，时间复杂度O(log_a)，所以整体时间复杂度O(K * log_C_k)，K为出现多少种牌，C_k为每种牌的出现次数。
