# 283. Move Zeroes

## 题目

>Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
>
>**Example:**
>
>>Input: [0,1,0,3,12]  
>>Output: [1,3,12,0,0]  
>
>**Note:**
>
> - You must do this **in-place** without making a copy of the array.
> - Minimize the total number of operations.

## 解法

有两个要求：不产生数组的拷贝，最小化操作次数。

先暴力求解，慢指针p1指向要交换的0，快指针从慢指针开始向后遍历找第一个不为0的数，两元素交换，直到快指针走到数列末尾。

```java
public void moveZeroes(int[] nums) {
       int p1 = 0 , p2 =0;
       while (p2 < nums.length -1) {
           while (nums[p1] != 0 && p1 < nums.length-1) p1++;
           for (p2= p1; nums[p2] == 0 && p2 < nums.length-1; p2++);
           int temp = nums[p2];
           nums[p2] = nums[p1];
           nums[p1] = temp;
           p1++;
       }
    }
```

实际上，可以只用一个指针指向最后一个非0元素，快指针向后遍历的过程中从后向前覆盖。最后把慢指针之后的元素清0即可。时间复杂度O(n)，空间O(1)

```java
public void moveZeroes(int[] nums) {
        int p1 =0;
        for (int i =0; i< nums.length; i++)
            if (nums[i] != 0)
                nums[p1++] = nums[i];
        for (int i = p1; i< nums.length; i++)
            nums[i] =0;
    }
```

考虑数列`[0,0,0,...,1]`，上述方法需要在覆盖第一个元素之后写入n-1个0，然而数列本身就是0，造成操作次数的无端增多。

要减少这些重复的操作，就是把覆盖改为交换。当快指针p2遇到第一个非0的数，将其与慢指针p1所指向的元素进行交换。如果当前p2指向的是0则跳向下一个。

```java
 public void moveZeroes(int[] nums) {
        for (int p1 =0, p2 =0; p2 < nums.length; p2++)
            if (nums[p2] != 0) {
                int temp = nums[p2];
                nums[p2] = nums[p1];
                nums[p1] = temp;
                p1++;
            }
    }
```
