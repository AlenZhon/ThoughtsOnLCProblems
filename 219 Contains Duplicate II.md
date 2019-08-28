# 219. Contains Duplicate II

## 题目

给定数组nums和正整数k，判断数组中是否存在相同元素，其下标距离不超过k。

>Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.
>
>**Example 1:**
>
>>Input: nums = [1,2,3,1], k = 3  
>>Output: true
>
>**Example 2:**
>
>>Input: nums = [1,0,1,1], k = 1  
>>Output: true
>
>**Example 3:**
>
>>Input: nums = [1,2,3,1,2,3], k = 2  
>>Output: false

## 解法

用一个HashMap存元素值和相同元素最近的下标值，将时间复杂度为O(n)。

```java
 public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer, Integer> number = new HashMap<Integer, Integer>();
        for (int i =0; i< nums.length; i++) {
            if (number.containsKey(nums[i])) {
                if (i - number.get(nums[i]) <=k) return true;
            }
            number.put(nums[i], i);
        }
        return false;
    }
```

看到别人的其他解法有用 HashSet 维护滑动窗口的。使用到了`add()`的特性——如果此 set 已包含该元素，则该调用不更改 set 并返回 `false`。在运行时间上稍微快一点点。

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> set = new HashSet<Integer>();
    for(int i = 0; i < nums.length; i++){
        if(i > k) set.remove(nums[i-k-1]);
        if(!set.add(nums[i])) return true;
    }
    return false;
}
```

还有人用两个下标`p1,p2`做遍历的（似乎感觉少比较了几次，但却可以通过）

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
       if(nums.length <= 1 || k <= 0) return false;
        int p1 = 0, p2 = 0;
        while(p1 < nums.length){
            if(p1 != p2 && nums[p1] == nums[p2]) return true;
            if(p2 - p1 < k && p2 < nums.length - 1) p2++;
            else p1++;
        }
        return false;
    }
```
