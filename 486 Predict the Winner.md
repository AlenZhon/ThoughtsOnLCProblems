# 486. Predict the Winner

## 题目

给定一个表示分数的非负整数数组。 玩家 1 从数组任意一端拿取一个分数，随后玩家 2 继续从剩余数组任意一端拿取分数，然后玩家 1 拿，…… 。每次一个玩家只能拿取一个分数，分数被拿取之后不再可取。直到没有剩余分数可取时游戏结束。最终获得分数总和最多的玩家获胜。

给定一个表示分数的数组，预测玩家1是否会成为赢家。你可以假设每个玩家的玩法都会使他的分数最大化。

```java
**示例 1：**

输入：[1, 5, 2]
输出：False
解释：一开始，玩家1可以从1和2中进行选择。
如果他选择 2（或者 1 ），那么玩家 2 可以从 1（或者 2 ）和 5 中进行选择。如果玩家 2 选择了 5 ，那么玩家 1 则只剩下 1（或者 2 ）可选。
所以，玩家 1 的最终分数为 1 + 2 = 3，而玩家 2 为 5 。
因此，玩家 1 永远不会成为赢家，返回 False 。

**示例 2：**

输入：[1, 5, 233, 7]
输出：True
解释：玩家 1 一开始选择 1 。然后玩家 2 必须从 5 和 7 中进行选择。无论玩家 2 选择了哪个，玩家 1 都可以选择 233 。
     最终，玩家 1（234 分）比玩家 2（12 分）获得更多的分数，所以返回 True，表示玩家 1 可以成为赢家。
```
 
**提示：**

- 1 <= 给定的数组长度 <= 20.
- 数组里所有分数都为非负数且不会大于 10000000 。
- 如果最终两个玩家的分数相等，那么玩家 1 仍为赢家。

## 思路与解法

首先理解题目。两个人交替拿数组里的头或者尾的数。如果暴力穷举，就得有2^n种拿取方式，想到递归的操作。

### 递归 

对于玩家1来说，当前选了x，赢了对方x分，在后面的游戏中，如果对方总共赢了y分并且x小于y，那么对方就赢了。

那么对于每一次递归，我们需要返回当前做选择的玩家赢过对手的分数。如果数组里只有一个数nums[i]可以取，那么当前玩家赢过对手的分数就是这个数nums[i].由于有两种取数方法，判断取最大值即可。

时间复杂度是O(2^n)，空间复杂度是O(n)，主要是递归的栈空间.

```java
class Solution {
    public int helper(int[] nums, int start, int end){
        if (start == end){
            return nums[start];
        }
        int pickStart = nums[start] - helper(nums, start + 1, end);
        int pickEnd = nums[end] - helper(nums, start, end - 1);
        return Math.max(pickEnd, pickStart);
    }
    public boolean PredictTheWinner(int[] nums) {
        return helper(nums, 0, nums.length - 1) >=0;
    }
}
```

### 缓存中间状态的递归

上面的递归时间复杂度太大，主要是因为重复计算了太多次相同的子问题。在递归树里每一次遇到区间[i, j]的子问题都得重新算一次。

我们把计算好的子问题结果放到score[][]数组里，遇到区间start,end的问题先去查数组，数组中有就直接返回，没有再去计算。

时间复杂度降到了O(n^2)，空间复杂度O(n^2)

```java
class Solution {
    private Integer[][] score;
    public int helper(int[] nums, int start, int end){
        if (start == end){
            return nums[start];
        } 
        if (!Objects.isNull(score[start][end])) return score[start][end];
        int pickStart = nums[start] - helper(nums, start + 1, end);
        int pickEnd = nums[end] - helper(nums, start, end - 1);
        score[start][end] = Math.max(pickEnd, pickStart);
        return score[start][end];
    }
    public boolean PredictTheWinner(int[] nums) {
        score = new Integer[nums.length][nums.length];
        for (int i = 0; i< score.length; i++){
            Arrays.fill(score[i], null);
        }
        return helper(nums, 0, nums.length - 1) >=0;
    }
}
```

### 动态规划

在上一种算法中我们已经可以看出问题具有重复子问题的特征，并且score[][]数组已经有动态规划内味了。考虑使用动态规划求解。

base case就是`dp[i][i] = nums[i]`
状态转移方程就是`dp[i][j] = Math.max(nums[i] - dp[i+1][j], nums[j] - dp[i][j-1])`

最后判断`dp[0][nums.length -1]>=0`
注意运算范围和方向， score[][]数组只用了对角线及以上（i<=j）,需要从数组右下角往上，左上角往右依次运算。这里也可以发现这就是一棵斜向的递归树，只不过我们从下自上运算。

时间复杂度和空间复杂度与算法2相同。
```java
public boolean PredictTheWinner(int[] nums) {
        Integer[][] dp = new Integer[nums.length][nums.length];
        for (int i = 0; i< nums.length; i++){
            dp[i][i] = nums[i];
        }
        for (int i = nums.length - 2; i>=0; i--){
            for (int j = i + 1; j < nums.length; j++){
                int pickStart = nums[i] - dp[i+1][j];
                int pickEnd = nums[j] - dp[i][j-1];
                dp[i][j] = Math.max(pickStart, pickEnd);
            }
        }
        return dp[0][nums.length - 1] >=0;
    }
```

#### 进一步优化空间

可以看到状态转移方程只需要两行的状态。把二维数组压缩成一维，然后从后向前更新即可完成相同的运算。

```java
public boolean PredictTheWinner(int[] nums) {
        Integer[] dp = new Integer[nums.length];
        for (int i = 0; i< nums.length; i++){
            dp[i] = nums[i];
        }
        for (int i = nums.length - 2; i>=0; i--){
            for (int j = i + 1; j < nums.length; j++){
                dp[j] = Math.max(nums[i] - dp[j], nums[j] - dp[j-1]);
            }
        }
        return dp[nums.length - 1] >=0;
    }
```

### Note

- 首先得想到用得分的差值去表示比赛的输赢，不然就会陷入递归的细节。
- 动态规划的状态转移方程可以从递归开始想。