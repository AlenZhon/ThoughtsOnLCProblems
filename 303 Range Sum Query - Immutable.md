# 303. Range Sum Query - Immutable

## 题目

给定一个Integer数组，计算索引值`[i,j]`的元素之和。假设数组元素不可变且计算元素和的次数很多。

>Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.
>
>**Example:**
>
>>Given nums = [-2, 0, 3, -5, 2, -1]
>>
>>sumRange(0, 2) -> 1  
>>sumRange(2, 5) -> -1  
>>sumRange(0, 5) -> -3
>
>**Note:**
>
> 1. You may assume that the array does not change.
> 2. There are many calls to sumRange function.

## 解法

既然题目已经明确指明了函数会调用多次，那么每次用一个for循环相加的暴力破解法肯定会超时。时间复杂度每次调用需要O(n)，空间复杂度O(1)。

空间换时间。由于数组元素不变，可以先计算`[0,j]`的元素之和存入缓存数组。

```java
class NumArray {

    private int[] sums;
    public NumArray(int[] nums) {
        sums = new int[nums.length + 1];
        int sum = 0;
        for (int i =0; i< nums.length; i++){
            sum += nums[i];
            sums[i + 1] = sum;
        }
    }

    public int sumRange(int i, int j) {
        if (i == 0) return sums[j+1];
        return sums[j+1]- sums[i];
    }
}
```

时间复杂度每次查询O(1)，空间复杂度O(n)。
