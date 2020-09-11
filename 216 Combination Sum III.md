# 216. Combination Sum III

## 题目

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：
- 所有数字都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**  

输入: k = 3, n = 7  
输出: [[1,2,4]]

**示例 2:**

输入: k = 3, n = 9  
输出: [[1,2,6], [1,3,5], [2,3,4]]

## 解法

回溯。时间复杂度是O(C^k_M * k) 本题中M固定为9，一共有 C^k_M 个组合，每次判断需要的时间代价是 O(k)。空间复杂度是O(M + k).

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> retList = new ArrayList<List<Integer>>();
        if (k ==0 || n ==0) return retList;
        helper(retList, k, n, new ArrayList<Integer>());
        return retList;
    }

    public void helper(List<List<Integer>> retList, int k , int n, List<Integer> tempList){
        if (tempList.size() == k && n == 0){
                retList.add(new ArrayList<>(tempList));
            return;
        }
        int start = (tempList.size() > 0) ? tempList.get(tempList.size() - 1) + 1 : 1;
        for (int i = start; i <= 9 && n- i >= 0; i++){
            tempList.add(i);
            helper(retList, k, n - i, tempList);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```