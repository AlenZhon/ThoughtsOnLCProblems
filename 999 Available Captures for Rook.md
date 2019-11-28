# 999. Available Captures for Rook

## 题目

`8*8`的国际象棋棋盘里有一只white rook。已知车的移动规则是选择上下左右四个方向之一进行直线移动，直到被自己的其他棋子挡住，或者到达棋盘边界，或者吃掉黑方的棋子并停留在黑方棋子的那一格。  
现在用一个`char[][]`表示棋盘上的棋子，只有四种种类，`'.'`表示空格，`'p'`表示black pawn，`'R'`表示white rook，`'B'`表示white bishop。你执白移动white rook一次，有多少种吃掉black pawn的可能？

>On an 8 x 8 chessboard, there is one white rook.  There also may be empty squares, white bishops, and black pawns.  These are given as characters 'R', '.', 'B', and 'p' respectively. Uppercase characters represent white pieces, and lowercase characters represent black pieces.
>
>The rook moves as in the rules of Chess: it chooses one of four cardinal directions (north, east, west, and south), then moves in that direction until it chooses to stop, reaches the edge of the board, or captures an opposite colored pawn by moving to the same square it occupies.  Also, rooks cannot move into the same square as other friendly bishops.
>
>Return the number of pawns the rook can capture in one move.
>
>
>**Example 1:**
>
>>Input:  
>>[`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".","p",".",".",".","."]`,
>>&nbsp;`[".",".",".","R",".",".",".","p"]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".","p",".",".",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`]  
>>Output: 3  
>>Explanation:
>>In this example the rook is able to capture all the pawns.
>
>**Example 2:**
>
>>Input:  
>>[`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".","p","p","p","p","p",".","."]`,
>>&nbsp;`[".","p","p","B","p","p",".","."]`,
>>&nbsp;`[".","p","B","R","B","p",".","."]`,
>>&nbsp;`[".","p","p","B","p","p",".","."]`,
>>&nbsp;`[".","p","p","p","p","p",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`]  
>>Output: 0  
>>Explanation:
>>Bishops are blocking the rook to capture any pawn.
>
>**Example 3:**
>
>>Input:  
>>[`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".","p",".",".",".","."]`,
>>&nbsp;`[".",".",".","p",".",".",".","."]`,
>>&nbsp;`["p","p",".","R",".","p","B","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`,
>>&nbsp;`[".",".",".","B",".",".",".","."]`,
>>&nbsp;`[".",".",".","p",".",".",".","."]`,
>>&nbsp;`[".",".",".",".",".",".",".","."]`]  
>>Output: 3  
>>Explanation:
>>The rook can capture the pawns at positions b5, d6 and f5.
>
>**Note:**
>
> - board.length == board[i].length == 8
> - board[i][j] is either 'R', '.', 'B', or 'p'
> - There is exactly one cell with board[i][j] == 'R'

## 解法

straight-forward。先找到R的位置，然后上下左右判断第一个非空的格子上是不是black pawn。

```java
public int numRookCaptures(char[][] board) {
        int rooki = 0, rookj = 0;
        for (int i = 0; i < 8; i++)
            for (int j = 0; j< 8; j++)
                if (board[i][j] == 'R') {
                    rooki = i;
                    rookj = j;
                }
        return check(board, rooki, rookj);
    }

    private int check(char[][] board, int rooki, int rookj){
        int count = 0, i = 0, j = 0;
        for (i = rooki - 1; i>= 0 && board[i][rookj] == '.'; i--);
        if (i >=0 && board[i][rookj] == 'p') count++;
        for (i = rooki + 1; i< 8 && board[i][rookj] =='.'; i++);
        if (i< 8 && board[i][rookj] == 'p') count++;
        for (j = rookj - 1; j>= 0 && board[rooki][j] == '.'; j--);
        if (j >=0 && board[rooki][j] == 'p') count++;
        for (j = rookj + 1; j< 8 && board[rooki][j] =='.'; j++);
        if (j< 8 && board[rooki][j] == 'p') count++;
        return count;
    }
```
