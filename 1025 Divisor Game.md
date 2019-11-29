# 1025. Divisor Game

## 题目

Alice和Bob在玩一个游戏。两个人都很聪明所以他们始终都按照最优解去玩。这个游戏初始给一个数N，由Alice开始选择一个整数 x 满足`0 < x < N && N % x == 0`，并用`N-x`替代 N 。两人交替选择，直到无法选择x的一方判输。现在给定N，Alice稳赢的话就返回真，反之返回假。

>Alice and Bob take turns playing a game, with Alice starting first.
>
>Initially, there is a number N on the chalkboard.  On each player's turn, that player makes a move consisting of:
>
> - Choosing any x with 0 < x < N and N % x == 0.
> - Replacing the number N on the chalkboard with N - x.
>
>Also, if a player cannot make a move, they lose the game.
>
>Return True if and only if Alice wins the game, assuming both players play optimally.
>
>**Example 1:**
>
>>Input: 2  
>>Output: true  
>>Explanation: Alice chooses 1, and Bob has no more moves.
>
>**Example 2:**
>
>>Input: 3  
>>Output: false  
>>Explanation: Alice chooses 1, Bob chooses 1, and Alice has no more moves.
>
>**Note:**
>
> - 1 <= N <= 1000

## 解法

根据题目意思，推几个例子可以发现，先手Alice偶数必胜，奇数必败。

证明：  
当N==2时，Alice的最优解（唯一解）就是选择1把Bob弄掉。  
当给定N为偶数时，Alice只需要每次选择 1，留下 N-1 为奇数。由于奇数的因子一定是奇数(如果有偶数因子那N就为偶数了)，奇数 - 奇数 = 偶数，所以Bob只能无奈地把一个偶数留给Alice。以此类推，Alice最后肯定会获得 N==2 的情况，从而把Bob弄掉。所以偶数时先手必胜。  
当给定N为奇数时，情况恰好相反。Bob根据最优解按照上面思路选择 1 得到一个偶数 N-1 送给Alice。这样Bob最后会获得 N==2 的情况，所以奇数时先手必败。

所以问题转化为了判断N的奇偶性。一行代码直接return就完事了。
