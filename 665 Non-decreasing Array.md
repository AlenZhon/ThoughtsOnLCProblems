# 665. Non-decreasing Array

## 题目

给定一个数组，判断它能否通过改变至多一个元素值，变成一个非递减数组。

>Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.
>
>We define an array is non-decreasing if `array[i] <= array[i + 1]` holds for every `i` (`1 <= i < n`).
>
>Example 1:
>
>>Input: [4,2,3]  
>>Output: True  
>>Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
>
>Example 2:
>
>>Input: [4,2,1]  
>>Output: False  
>>Explanation: You can't get a non-decreasing array by modify at most one element.
>
>**Note:** The n belongs to `[1, 10,000]`.

## 解法

想到了一个破坏原数组的解法。  
遍历数组，当第一次看到一个需要修改的元素a[i]，比较该元素相邻的a[i-1], a[i+1]的大小，修改这三个元素的值使之非递减，并标记已经修改过一次。如果还需要修改就直接`return false`。

时间复杂度O(n) 空间O(1)

```java
public boolean checkPossibility(int[] nums) {
        if (nums.length == 1) return true;
        boolean decrease = true;
        for (int i = 0; i< nums.length - 1; i++) {
            if (nums[i] > nums[i + 1]) {
                if (i > 0)
                    if (nums[i - 1] <= nums[i + 1]) nums[i] = nums[i - 1];
                    else nums[i + 1] = nums[i];
                if (decrease) decrease = false;
                else return false;
            }
        }
        return true;
    }
```

或者用`previous` 保存前一个元素（如果要修改就保存修改后的）

```java
     public boolean checkPossibility(int[] nums) {
        int previous = Integer.MIN_VALUE;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] >= previous) {
                previous = nums[i];
            } else {
                if (count == 0) {
                    count++;
                    if (i < 2) {
                        previous = nums[1];
                        continue;
                    }
                    if (i >= 2 && nums[i] >= nums[i-2]) {
                        previous = nums[i];
                        continue;
                    }
                    if (i < nums.length-1 && nums[i-1] <= nums[i+1]) {
                        previous = nums[i-1];
                        continue;
                    }
                    if (i == nums.length-1) return true;
                    else return false;
                }
                else return false;
            }
        }
        return true;
    }
```
