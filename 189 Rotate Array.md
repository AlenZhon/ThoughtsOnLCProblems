# 189. Rotate Array

## 题目描述

给定一个数组，求该数组循环右移k次后的结果。

>Given an array, rotate the array to the right by k steps, where k is non-negative.
>
>>Example 1:
>>
>>Input: [1,2,3,4,5,6,7] and k = 3  
>>Output: [5,6,7,1,2,3,4]  
>>Explanation:  
>>rotate 1 steps to the right: [7,1,2,3,4,5,6]  
>>rotate 2 steps to the right: [6,7,1,2,3,4,5]  
>>rotate 3 steps to the right: [5,6,7,1,2,3,4]
>>
>>Example 2:
>>
>>Input: [-1,-100,3,99] and k = 2  
>>Output: [3,99,-1,-100]  
>>Explanation:  
>>rotate 1 steps to the right: [99,-1,-100,3]  
>>rotate 2 steps to the right: [3,99,-1,-100]
>
>Note:
>
> - Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
> - Could you do it in-place with O(1) extra space?

## 怎么写的

提示说至少有三种方法。肯定有一种暴力循环的方法，用一个变量存右移出来的元素。时间复杂度O(n*k)，空间复杂度O(1)，但是太慢了。

先不考虑in-place with O(1) extra space的进阶要求，把一个变量拓展成一个`int[nums.length]`数组，把`nums[i]`放在对应下标`[(i+k)%nums.length]`的位置上。时间复杂度O(n),两次循环。空间复杂度O(n)。

```java
public void rotate(int[] nums, int k) {
        int[] a = new int[nums.length];
        for (int i = 0 ; i< nums.length; i++) {
            a[(i+k) % nums.length] = nums[i];
        }
        for (int i = 0 ; i< nums.length; i++) {
            nums[i] = a[i];
        }
    }
```

如果要满足进阶要求，只能在数组内部做元素的交换。考虑到当`k>n`时，循环右移`k`次和循环右移`k%n`次是相等的。Approach #3 Using Cyclic Replacements使用了循环交换的方法，先记录下`num[i+k]`的值，再把前一次记录下的`nums[i]`移到`num[i+k]`，比如数组`[1,2,3,4,5,6,7], k=3`，则循环交换所记录下的元素依次是`4->7->3->6->2->5->`。

不过这个方法有一个坑。当`n % k == 0`时，一轮循环下来只移动了n/k个元素。比如数组`[1,2,3,4,5,6], k=2`，就需要两次循环`3->5->`和`2->4`。代码中使用了`count`用来记录移动的次数，解决了这个情况。如果遇到上述情况一轮循环交换过后`count==3`，使得i自增1进入第二轮循环。时间复杂度O(n)，空间复杂度O(1)。

```java
public void rotate(int[] nums, int k) {
        int count = 0;
        k = k % nums.length;
        for (int i = 0; count < nums.length; i++) {
            int j = i;
            int prev = nums[i];
            do {
                j = (j+k) % nums.length;
                int temp = nums[j];
                nums[j] = prev;
                prev = temp;
                count++;
            } while (j != i);
        }
    }
```

第四种方法是使用了翻转数组的思想。一个数组循环右移k次，相当于连续进行了三次翻转数组，先翻转整个数组，再翻转前k个元素，翻转后n-k个元素。n个元素被交换了三次，时间复杂度为O(n)，空间复杂度为O(1)。

```java
k %= nums.length; //不要忘记这一步
reverse(nums,0,nums.length-1);
reverse(nums,0,k-1);
reverse(nums,k-1,nums.length-1);

public void reverse(int[] nums, int start, int end)
```
