# 292. Nim Game

## 题目

有一堆石头，石头的总数为n。你和对手轮流从石堆里取石头，每人每次只允许拿1块、2块或3块石头，最后把石堆拿完的人为赢家。假设你和你的对手都很聪明，每次都按最优方案进行游戏，在给定总数n时，判断如果你先手是否最终会赢。

>You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.
>
>Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.
>
>**Example:**
>
>>Input: 4  
>>Output: false  
>>Explanation: If there are 4 stones in the heap, then you will never win the game;  
>>No matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

## 解法

容易看出在题给条件下问题可迭代。如果n=5, 6, 7，只需分别拿取1，2，3块石头即可将必输策略转化给对手。而n = 8时，不管拿1，2，3块石头，对于对手来说都是必赢的。

数学归纳法可证明当n是4的倍数时必输。

`return (n % 4 != 0)`即可。
