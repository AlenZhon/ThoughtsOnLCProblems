# 16. 3Sum Closest

## 题目

给定一个数组nums和一个目标数字 target。找出数组中的三元组 <x, y, z> 使得三个数之和最接近target。输出这三个数之和。

>Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
>**Example:**
>
>>Given array nums = [-1, 2, 1, -4], and target = 1.
>>
>>The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

## 解法

和 *15 3sum* 想法一样，还是用two-pointer。时间复杂度O(n^2) (5ms)

```java
public int threeSumClosest(int[] nums, int target) {
        int diff = Integer.MAX_VALUE, sum = 0;
        Arrays.sort(nums);
        for (int i = 0; i< nums.length -2; i++){
            int left = i+1, right = nums.length - 1;
            while (left < right){
                if (Math.abs(target - (nums[i] + nums[left] + nums[right])) < diff){
                    diff = Math.abs(target - (nums[i] + nums[left] + nums[right]));
                    sum = nums[i] + nums[left] + nums[right];
                }
                if (nums[i] + nums[left] + nums[right] == target) return target;
                else if (nums[i] + nums[left] + nums[right] > target) right--;
                else left++;
            }
        }
        return sum;
    }
```
