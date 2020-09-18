# 47. Permutations II

## 题目

给定一个可包含重复数字的序列，返回所有不重复的全排列。

```java
示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```


## 解法

回溯算法。和 46题大体思路相同。如何解决不重复的问题？

设定**重复元素只被填入一次**。具体来说，首先对原数组排序使得重复元素相邻，之后对于每次填入，一定是这些重复元素中从左到右第一个没被填过的数字。

```java
if (i > 0 && nums[i] == nums[i - 1] && !vis[i - 1]) {
    continue;
}
```

时间复杂度为O(n * n!)。回溯算法的调用次数收到n的部分排列制约，计算累加式得到O(n!)。而每个调用都需要把list添加到数组里去，复制需要O(n)。

空间复杂度需要O(n)的`visited`数组，并且受递归深度影响，可知复杂度与序列长度有关O(n)。

```java
 public void helper(int[] nums, boolean[] visited, List<List<Integer>> retList,
                         List<Integer> list, int index){
        int n = nums.length;
        if (index == n){
            retList.add(new ArrayList<Integer>(list));
            return;
        }
        for (int i = 0; i< n; i++){
            if (visited[i] || (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1])) 
                continue;
            visited[i] = true;
            list.add(nums[i]);
            helper(nums, visited, retList, list, index + 1);
            visited[i] = false;
            list.remove(index);
        }
    }
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        int n = nums.length;
        boolean[] visited = new boolean[n];
        Arrays.sort(nums);
        helper(nums, visited, ret, new ArrayList<Integer>(), 0);
        return ret;
    }
```