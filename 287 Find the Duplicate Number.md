# 287. Find the Duplicate Number

## 题目

给定一个含有n+1个整数的数组，每个整数均在`[1, n]`的范围内。证明至少有一个数字是重复的，并找出该重复数字。

>Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.
>
>**Example 1:**
>
>>Input: [1,3,4,2,2]  
>>Output: 2  
>
>**Example 2:**
>
>>Input: [3,1,3,4,2]  
>>Output: 3  
>
>**Note:**
>
> - You must not modify the array (assume the array is read only).
> - You must use only constant, O(1) extra space.
> - Your runtime complexity should be less than O(n^2).
> - There is only one duplicate number in the array, but it could be repeated more than once.

## 解法

证明可由抽屉原理给出。

由于**Note**里提到了很多要求，所以既不能排序之后找相邻元素是否相等（数列只读，空间复杂度），也不能新引入HashSet等数据结构（空间复杂度）。放弃思考。

Solution给出的解法叫做`Floyd's Tortoise and Hare (Cycle Detection)`。由于数组元素在`[1, n]`范围内，可将数组看成链表的结构，第i个下标存储的元素指向第v_i个下标。那么整个题目就转化为链表寻找自环入口 *#142 Linked List Cycle II* 的题目。根据证明，自环必存在，只需找到自环入口即可。

这个思路转化得非常精彩，学习到了。

```java
 public int findDuplicate(int[] nums) {
        int slow = nums[0], fast = nums[0];
        do {
            fast = nums[nums[fast]];
            slow = nums[slow];
        } while (slow != fast);
        int temp = nums[0];
        while (slow != temp) {
            slow = nums[slow];
            temp = nums[temp];
        }
        return slow;
    }
```
