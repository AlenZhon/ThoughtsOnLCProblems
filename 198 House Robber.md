# 198. House Robber

## 题目

你是一个沿街偷东西的小偷，事先知道一条街上所有房屋里的现金，并且知道这条街的安保系统有如下性质：如果一间房屋的相邻两家都被偷了则自动报警。问如何行动使得在不触发警报的前提下偷到最多钱。

>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**
>
>Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police.**
>
>>**Example 1:**
>>
>>**Input:** [1,2,3,1]  
>>**Output:** 4  
>>**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).  
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Total amount you can rob = 1 + 3 = 4.
>>
>>**Example 2:**
>>
>>**Input:** [2,7,9,3,1]  
>>**Output:** 12  
>>**Explanation:** Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).  
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Total amount you can rob = 2 + 9 + 1 = 12.

## 怎么写的

乍一看以为分奇偶下标比较即可，但考虑到某些情况（如[2,1,1,10,8]最佳方案偷2+10）就发现和奇偶无关。

考虑用动态规划的想法。设定一个rob数组两个元素，遍历到第i个房屋时，`rob[0]`存储的是前i-2个房屋的所能偷到的最大值，`rob[1]`存储前i-1个房子所能偷到的最大值。`rob[1]`根据`max(rob[1] , rob[0]+nums[i])`更新，分别表示“不偷这个屋子，继续选择之前方案”和“偷这个屋子并选择前i-2房屋的方案”。

```java
public int rob(int[] nums) {
        if (nums.length <=0) return 0;
        else if (nums.length == 1) return nums[0];
        int[] rob = new int[]{nums[0], Math.max(nums[0], nums[1])};
        for (int i = 2; i< nums.length; i++) {
            int temp = rob[1];
            rob[1] = Math.max(rob[0] + nums[i], rob[1]);
            rob[0] = temp;
        }
        return rob[1];
}
```

动态规划大法nb。
