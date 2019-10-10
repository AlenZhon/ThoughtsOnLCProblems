# 532. K-diff Pairs in an Array

## 题目

给定一个数组，要求找出满足如下条件的`(i,j)`元素对：元素`i`和元素`j`之间的绝对距离是`k`。

>Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.
>
>**Example 1:**
>
>>Input: [3, 1, 4, 1, 5], k = 2  
>>Output: 2  
>>Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).  
Although we have two 1s in the input, we should only return the number of unique pairs.
>
>**Example 2:**
>>
>>Input:[1, 2, 3, 4, 5], k = 1  
>>Output: 4  
>>Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
>
>**Example 3:**
>
>>Input: [1, 3, 1, 5, 4], k = 0  
>>Output: 1  
>>Explanation: There is one 0-diff pair in the array, (1, 1).
>
>**Note:**
>
> - The pairs (i, j) and (j, i) count as the same pair.
> - The length of the array won't exceed 10,000.
> - All the integers in the given input belong to the range: [-1e7, 1e7].

## 解法

一个HashMap解决问题。时间复杂度`O(m+n)`，其中m是数组元素个数，n是数组不重复元素的个数。空间复杂度`O(n)`

然而边界情况欠考虑：第一次没有考虑到`k == 0`时算的是有哪些数字发生了重复。第二次没有想到还会给`k < 0`的测试用例。

```java
 public int findPairs(int[] nums, int k) {
        if (nums.length <=1 || k < 0) return 0;
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i : nums)
            map.put(i, map.getOrDefault(i, 0) + 1);
        Set<Integer> keySet = map.keySet();
        if (k == 0) {
            int dup = 0;
            for (Integer curr : keySet)
                if (map.get(curr) > 1) dup++;
            return dup;
        }

        int count = 0;
        for (Integer curr : keySet)
            if (keySet.contains(curr + k)) count++;
        return count;
    }
```

还可以用排序加双指针来做。时间复杂度`O(m)`，空间`O(1)`

```java
public int findPairs(int[] nums, int k) {
        if (nums.length <=1 || k < 0) return 0;
        Arrays.sort(nums);
        int left = 0, right = 1, count =0;
        while (right < nums.length) {
            if (nums[right] - nums[left] > k)
                left++;
            else if (nums[right] - nums[left] < k || left == right)
                right++;
            else {
                count++;
                left++;
                right++;
                while(right < nums.length && nums[right] == nums[right - 1])
                    right++;
            }
        }
        return count;
    }
```
