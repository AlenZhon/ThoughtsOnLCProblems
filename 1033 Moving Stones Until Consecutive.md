# 1033. Moving Stones Until Consecutive

## 题目

在自然数数轴上有三块石头，分别放在不同的数上。每次挪动一块石头离开原先的位置到一个新的数上称为一次操作。问最少通过几次操作可将三块石头挪到相邻的三个自然数上？最多需要几次？

>Three stones are on a number line at positions a, b, and c.
>
>Each turn, you pick up a stone at an endpoint (ie., either the lowest or highest position stone), and move it to an unoccupied position between those endpoints.  Formally, let's say the stones are currently at positions x, y, z with x < y < z.  You pick up the stone at either position x or position z, and move that stone to an integer position k, with x < k < z and k != y.
>
>The game ends when you cannot make any more moves, ie. the stones are in consecutive positions.
>
>When the game ends, what is the minimum and maximum number of moves that you could have made?  Return the answer as an length 2 array: `answer = [minimum_moves, maximum_moves]`
>
>Example 1:
>
>>Input: `a = 1, b = 2, c = 5`  
>>Output: `[1,2]`  
>>Explanation: Move the stone from 5 to 3, or move the stone from 5 to 4 to 3.
>
>**Example 2:**
>
>>Input: `a = 4, b = 3, c = 2`  
>>Output: `[0,0]`  
>>Explanation: We cannot make any moves.
>
>**Example 3:**
>
>>Input: `a = 3, b = 5, c = 1`  
>>Output: `[1,2]`  
>>Explanation: Move the stone from 1 to 4; or move the stone from 1 to 2 to 4.
>
>**Note:**
>
> - `1 <= a <= 100`
> - `1 <= b <= 100`
> - `1 <= c <= 100`
> - `a != b, b != c, c != a`

## 解法

一道脑筋急转弯类型的题目。  
最少的次数只会出现在`[0, 1, 2]`三个数之间。

- 0: 三个石头本身就相邻
- 1：其中两个石头相邻/其中两个石头中间空了一格
- 2：其他情况

最多的次数就和三个石头最初的差值有关。`diff2 + diff1 - 2`。

```java
public int[] numMovesStones(int a, int b, int c) {
        int z = Math.max(a, Math.max(b, c));
        int x = Math.min(a, Math.min(b, c));
        int y = a + b + c - x - z;
        int diff1 = y - x, diff2 = z - y;
        if (diff1 == 1 && diff2 == 1)
            return new int[]{0, diff1 + diff2 - 2};
        else if (diff1 == 2 || diff2 == 2 || diff1 == 1 || diff2 == 1)
            return new int[]{1, diff1 + diff2 - 2};
        return new int[]{2, diff1 + diff2 - 2};
    }
```
