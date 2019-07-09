# 26 Remove Duplicates from Sorted Array

## 题目描述

给定一个已经排序好的数列，要求将其中重复的元素移除，并输出新数列的长度。要求空间复杂度O(1)。

>Clarification:  
>Confused why the returned value is an integer but your answer is an array?
>
>Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.
>
>Internally you can think of this:
>
>```java
>// nums is passed in by reference. (i.e., without making a copy)
>int len = removeDuplicates(nums);
>
>// any modification to nums in your function would be known by the caller.
>// using the length returned by your function, it prints the first len elements.
>for (int i = 0; i < len; i++) {
>    print(nums[i]);
>}
>```

## 示例

>Example 1:
>
>Given nums = [1,1,2],
>
>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
>
>It doesn't matter what you leave beyond the returned length.
>
>Example 2:
>
>Given nums = [0,0,1,1,1,2,2,3,3,4],
>
>Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
>
>It doesn't matter what values are set beyond the returned length.

## 思路

示例已经给出了提示。
>It doesn't matter what you leave beyond the returned length.

由于已经是一个排好序的数列，既然只返回新数列的长度，又不能申请空间，再看到Clarification的示例把不重复的元素置于数列开头，那么想法已经很清楚了。

用两个指针`i,j`分别指向当前最后一个不重复元素和待比较的元素。如果`nums[j]!= nums[i]` 那么让i指向下一个元素，并用当前的nums[j]赋值。这样`j`可以跳过所有当前不重复的元素，因此时间复杂度为O(n)。时间最长的情况为所有数组元素都不重复，i,j均走过n。
