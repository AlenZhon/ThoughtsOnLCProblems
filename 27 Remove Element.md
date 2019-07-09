# 27 Remove Element

## 题目描述

>Given an array nums and a value val, remove all instances of that value in-place and return the new length.
>
>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
>
>The order of elements can be changed. It doesn't matter what you leave beyond the new length.
>
>Example 1:
>
>Given nums = [3,2,2,3], val = 3,
>
>Your function should return length = 2, with the first two elements of nums being 2.
>
>It doesn't matter what you leave beyond the returned length.
>
>Example 2:
>
>Given nums = [0,1,2,2,3,0,4,2], val = 2,
>
>Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.
>
>Note that the order of those five elements can be arbitrary.
>
>It doesn't matter what values are set beyond the returned length.

## 我的解法

和#26 几乎一样，用两个指针，只是从数组的第一个元素开始比即可。时间复杂度为O(n), 最坏的情况是两个指针元素都遍历了一遍，空间复杂度为O(1)

## 其他解法

考虑如果要移除的元素极少（只有一两个），且输出结果不追究原有顺序，可将第二个指针从后往前遍历，如果前指针所指元素需要移除，则把后指针向前移动，元素赋值给前指针，否则前指针向后移动直到两者相遇。

```java
public int removeElement(int[] nums, int val) {
    int i = 0;
    int n = nums.length;
    while (i < n) {
        if (nums[i] == val) {
            nums[i] = nums[n - 1];
            // reduce array size by one
            n--;
        } else {
            i++;
        }
    }
    return n;
}
```
