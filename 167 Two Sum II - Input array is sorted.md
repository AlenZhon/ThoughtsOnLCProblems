# 167 Two Sum II - Input array is sorted

## 题目描述

给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2，且下标从1开始。

>**示例:**
>
>**输入:** numbers = [2, 7, 11, 15], target = 9
>**输出:** [1,2]
>**解释:** 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。

## 怎么解的

双指针法，做就完事了。时间复杂度顶死了O(n)。

```java
public int[] twoSum(int[] numbers, int target) {
        int index1 = 0, index2 = numbers.length - 1;
        while (index1 < index2) {
            if (numbers[index1]+ numbers[index2] == target) {
                 return new int[]{1+index1, 1+index2};
            } else if (numbers[index1] + numbers[index2] > target) {
                index2 --;
            } else {
                index1 ++;
            }
        }
        return null;
    }
```
