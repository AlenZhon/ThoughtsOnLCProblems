# 747. Largest Number At Least Twice of Others

## 题目

一个数组中总是有最大的元素。如果这个最大值大于次大值的2倍则返回最大值的下标，否则返回-1。

>In a given integer array nums, there is always exactly one largest element.
>
>Find whether the largest element in the array is at least twice as much as every other number in the array.
>
>If it is, return the index of the largest element, otherwise return -1.
>
>**Example 1:**
>
>>Input: nums = [3, 6, 1, 0]  
>>Output: 1  
>>Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.
>
>**Example 2:**
>
>>Input: nums = [1, 2, 3, 4]  
>>Output: -1  
>>Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.
>
>Note:
>
> - nums will have a length in the range [1, 50].
> - Every nums[i] will be an integer in the range [0, 99].

## 解法

这题目有点不太清楚，没交代数列中元素是否unique。如果最大值在数列中出现了多次应该怎么办？测试了一下`[3,6,6,1,0]`，OJ返回的答案是1，也就是它是在数列中distinct element找的最大值，而且返回的是最靠左边的下标。

粗暴的方法可以先排序，对最大和次大值做判断。时间复杂度O(nlogn)，如果是in-place排序那么空间复杂度是O(1)。

也可以直接用遍历。首先遍历数列找到最大值及其下标，然后再遍历一次，如果发现有其他值的两倍大于最大值则返回-1.

```java
public int dominantIndex(int[] nums) {
        int maxIndex = -1, max = -1;
        for (int i = 0; i < nums.length; i++)
            if (nums[i] > max) {
                max = nums[i];
                maxIndex = i;
            }
        for (int num : nums)
            if (num != max && num * 2 > max) return -1;
        return maxIndex;
    }
```

进一步地， 可以通过一次遍历找到最大值和次大值。

```java
public int dominantIndex(int[] nums) {
        int maxIndex, secIndex;
        if (nums.length == 1) return 0;
        if (nums[0] > nums[1]) {
            maxIndex = 0;
            secIndex = 1;
        } else {
            maxIndex = 1;
            secIndex = 0;
        }
        for (int i = 2; i < nums.length; i++)
           if (nums[i] > nums[maxIndex]) {
               secIndex = maxIndex;
               maxIndex = i;
           } else if (nums[i] > nums[secIndex] && nums[i] != nums[maxIndex]) //如果元素unique 则第二个判断条件可以去掉
               secIndex = i;
        return nums[maxIndex] >= nums[secIndex] * 2 ? maxIndex : -1;
    }
```
