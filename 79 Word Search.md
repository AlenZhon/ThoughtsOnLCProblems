# 79. Word Search

## 题目

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。


**示例:**

```java
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```
 
**提示：**
-  `board` 和 `word` 中只包含大写和小写英文字母。
- 1 <= `board.length` <= 200
- 1 <= `board[i].length` <= 200
- 1 <= `word.length` <= 10^3

## 解法

回溯算法。

时间复杂度的上界应该为O(M*N*(3^L))，分别为矩阵的行数，列数，和字符串长度。由于剪枝的存在远小于这个上界。  
空间复杂度为O(MN)，因为额外开辟了visited数组用于存储访问状态。递归调用栈的最大深度为O(L)

```java
class Solution {
    public boolean helper(char[][] board, String word, boolean[][] visited, int i, int j, int index){
        if (index == word.length()) return true;
        if (i < 0 || j < 0 || j >= board[0].length || i >= board.length || board[i][j] != word.charAt(index) || visited[i][j]){
            return false;
        }
        visited[i][j] = true;
        boolean flag = helper(board, word, visited, i - 1, j, index + 1) ||
                        helper(board, word, visited, i, j - 1, index + 1) ||
                        helper(board, word, visited, i, j + 1, index + 1) ||
                        helper(board, word, visited, i + 1, j, index + 1);
        visited[i][j] = false;
        return flag;            
    }
    public boolean exist(char[][] board, String word) {
        boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i =0; i< board.length; i++){
            for (int j =0; j< board[0].length; j++){
                    if (helper(board, word, visited, i, j, 0)){
                        return true;
                    }
            }
        }
        return false;
    }
}
```
