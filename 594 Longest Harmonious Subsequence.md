# 594. Longest Harmonious Subsequence

## 题目

定义`harmounious array`为最大值与最小值相差恰好为1的数列。给定一个数列，在该数列的所有`subsequences`中找出最长的`harmounious array`。

>We define a harmounious array as an array where the difference between its maximum value and its minimum value is **exactly** 1.
>
>Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.
>
>**Example 1:**
>
>>Input: [1,3,2,2,5,2,3,7]  
>>Output: 5  
>>Explanation: The longest harmonious subsequence is [3,2,2,2,3].
>
>**Note:** The length of the input array will not exceed 20,000.

## 解法

求所有subsequences，再一个个判断的解法时间复杂度是n的幂级数，肯定是不行的。

想到HashMap，先记录下每个元素出现的次数，再寻找相邻两个key出现次数之和的最大值。时间复杂度O(n)，一次记录次数，一次遍历找最大值。空间复杂度也为O(n)。

```java
public int findLHS(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int num : nums)
            map.put(num, map.getOrDefault(num, 0) + 1);
        int length = 0;
        for (Integer key : map.keySet())
            if (map.containsKey(key + 1))
                length = Math.max(length, map.get(key) + map.get(key + 1));
        return length;
    }
```

如果对nums顺序不做要求的时候，可以进行排序。排序后相邻的元素相差最小。用`left`和`right`作为当前数列的左右下标。时间复杂度O(nlogn)。

```java
public int findLHS(int[] nums) {
        Arrays.sort(nums);

        int result = 0;
        int left = 0, right = 0;
        while(right < nums.length) {
            while(nums[right] - nums[left] > 1) {
                left++;
            }

            if(right- left + 1 > result && nums[right] - nums[left] == 1) {
                result = right - left + 1;
            }
            right++;
        }

        return result;
    }
```

实际上，使用HashMap的方法可以只使用一次遍历完成。在添加`key-value`的同时我们判断`(key + 1)`和`(key - 1)`的出现次数。时间复杂度和空间复杂度都是O(n)。

```java
public int findLHS(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int length = 0;
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
            if (map.containsKey(num + 1))
                length = Math.max(length, map.get(num) + map.get(num + 1));
            if (map.containsKey(num - 1))
                length = Math.max(length, map.get(num) + map.get(num - 1));
        }
        return length;
    }
```
