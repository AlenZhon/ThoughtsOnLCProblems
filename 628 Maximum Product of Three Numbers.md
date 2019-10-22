# 628. Maximum Product of Three Numbers

## 题目

一个数列，找出其中任意三个数之积的最大值。数列元素范围在`[-1000, 1000]`。三个数之积不会超过32位无符号整数的范围。

>Given an integer array, find three numbers whose product is maximum and output the maximum product.
>
>Example 1:
>
>>Input: [1,2,3]  
>>Output: 6
>
>Example 2:
>
>>Input: [1,2,3,4]
>>Output: 24
>
>**Note:**
>
> - The length of the given array will be in range `[3, 10^4]` and all elements are in the range `[-1000, 1000]`.
> - Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.

## 解法

先排个序咯。由于含有负数，比较一下最大的两个负数之积和第二第三大的两个正数之积哪个大。

```java
public int maximumProduct(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        if (nums[0] < 0 && nums[1] < 0 && nums[0] * nums[1] > nums[n-3] * nums[n-2])
            return nums[0] * nums[1] * nums[n-1];
        else
            return nums[n-1] * nums[n-2] * nums[n-3];
    }
```

时间复杂度是排序时的O(nlogn)。

直接遍历找最大的三个数和最小的两个数，时间复杂度O(n)

```java
public int maximumProduct(int[] nums) {
        int max1 = Integer.MIN_VALUE;
        int max2 = Integer.MIN_VALUE;
        int max3 = Integer.MIN_VALUE;
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        for (int num : nums) {
            if (num < min2) {
                if (num > min1) min2 = num;
                else {
                    min2 = min1;
                    min1 = num;
                }
            }
            if (num > max3) {
                if (num < max2) max3 = num;
                else if (num < max1) {
                    max3 = max2;
                    max2 = num;
                }
                else {
                    max3 = max2;
                    max2 = max1;
                    max1 = num;
                }
            }
        }
        return (max2 * max3 > min1 * min2) ? max2* max3 * max1 : min1 * min2 * max1;
    }
```
