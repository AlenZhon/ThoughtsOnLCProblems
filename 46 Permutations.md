# 46. Permutations

## 题目

给定一个 **没有重复** 数字的序列，返回其所有可能的全排列。

```java
示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## 解法

回溯算法。

时间复杂度为O(n * n!)。回溯算法的调用次数收到n的部分排列制约。而每个调用都需要把list添加到数组里去，复制需要O(n)。

空间复杂度受递归深度影响，可知复杂度与序列长度有关O(n)。

```java
public void helper(int[] nums, boolean[] visited, List<List<Integer>> retList,
                         List<Integer> list, int index){
        int n = nums.length;
        if (index == n){
            retList.add(new ArrayList<Integer>(list));
            return;
        }
        for (int i = 0; i< n; i++){
            if (visited[i]) continue;
            visited[i] = true;
            list.add(nums[i]);
            helper(nums, visited, retList, list, index + 1);
            visited[i] = false;
            list.remove(index);
        }
    }
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        boolean[] visited = new boolean[nums.length];
        helper(nums, visited, ret, new ArrayList<Integer>(), 0);
        return ret;
    }
```