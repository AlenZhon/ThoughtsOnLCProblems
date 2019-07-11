# 35 Search Insert Position

## 题目描述

给定一有序数列和一目标，若目标在数列中，返回其索引值；若不在数列中，则返回它按序插入到数列中的索引值。

可假设数列元素均不重复。

## 怎么解的

二分查找。

可以分递归和非递归写法，两种写法的时间复杂度O(log_{2} n), 非递归方法的空间复杂度为O(1)。

```java
public int searchInsert(int[] nums, int target) {
        int left= 0, right = nums.length -1;
        if (nums[left] > target) {return 0;}
        if (nums[right] < target) {return right+1;}
        while (left<= right) {
            int middle = (left + right) / 2;
            if (nums[middle]< target) {
                left = middle + 1;
            } else if (nums[middle] > target) {
                right = middle -1;
            } else if (nums[middle] == target) {
                return middle;
            }
        }
        return left;
    }
```
