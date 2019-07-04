# Two Sum

## 题目描述

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

例如： `nums = {2, 7, 11, 15} target = 9` 要求输出 `[0,1]`

## 解题思路

暴力破解就两层循环，时间复杂度为O(n^2)

如果以空间换时间，先将所有值存入HashMap再找，将查找的时间将为O(1)，空间复杂度为O(n)，而整体时间复杂度降为O(n)

使用HashMap (此处可引申 HashMap HashTable的相关知识)

## Trick & Notes

- HashMap的键存储为数组元素，值存为下标（反过来存则不好取`target- nums[i]`值所对应的键）
- `target- nums[i]` 不能是`nums[i]`本身！ 防止出现6-3 =3 的情况（但nums数组中可以有两个3）
- 可以将存值和检查的两次遍历并成一个，注意输出的先后顺序即可
- 如果找不到则 `throw new IllegalArgumentException("No solution");`
