# 645. Set Mismatch

## 题目

一个长度为n的数组中存储着`1..n`的正整数。但是由于数据错误，其中有一个元素a错误地变成了另一个元素b，造成了数组中有两个b而缺了a。给定数组，找到`(b, a)`

>The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.
>
>Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.
>
>Example 1:
>
>>Input: nums = `[1,2,2,4]`  
>>Output: `[2,3]`
>
>**Note:**
>
> - The given array size will in the range [2, 10000].
> - The given array's numbers won't have any order.

## 解法

第一反应是想到那道“1..n的数列中缺一个数”的问题。那里用的是异或解法。考虑这里是不是也可以这么用？

推了一波不太行。。。

数值`[1..n]`和`[0..n-1]`大部分是一一对应的，就缺了我们要求的那两个数。

可以对nums数组做标记的情况下，对每个`nums[i]`，判断`nums[Math.abs(nums[i] - 1)]`是否小于0，如果不小于0则乘上-1做个标记。这样遍历，因为总存在两个数相等，即`nums[i] == nums[j]`，当遍历到j时就会发现对应的`nums[Math.abs(nums[i] - 1)]`必定小于0。于是这个重复元素就被找出来了。

缺失的元素可以通过`sum(nums) - sum(array{1..n})`间接求出。

```java
public int[] findErrorNums(int[] nums) {
        int dup = 0 , miss = 0;
        for (int i = 0; i< nums.length; i++) {
            miss += i + 1 - Math.abs(nums[i]);
            if (nums[Math.abs(nums[i]) - 1] < 0)
                dup = Math.abs(nums[i]);
            else
                nums[Math.abs(nums[i]) - 1] *= -1;
        }
        return new int[]{dup, dup + miss};
    }
```

时间复杂度O(n)， 空间O(1)。
如果不能对nums进行修改，那就得新开一个boolean数组。空间复杂度增加为O(n)。

```java
public static int[] findErrorNums(int[] nums) {
        int size = nums.length;
        boolean[] tmp = new boolean[size];
        int dup = 0, missing = 0;
        for (int i = 0; i < size; i++) {
            if (tmp[nums[i] - 1]) {
                dup = nums[i];
            }
            else {
                tmp[nums[i]-1] = true;
            }

        }

        for (int i = 0; i < size; i++){
            if (!tmp[i]) {
                missing = i+1;
                break;
            }
        }
        return new int[]{dup, missing};
    }
```

刚才说的异或运算其实也可以解，就是有些麻烦。

```java
public int[] findErrorNums(int[] nums) {
        int xor = 0, xor0 = 0, xor1 = 0;
        for (int n: nums)
            xor ^= n;
        for (int i = 1; i <= nums.length; i++)
            xor ^= i;
        int rightmostbit = xor & ~(xor - 1);
        for (int n: nums) {
            if ((n & rightmostbit) != 0)
                xor1 ^= n;
            else
                xor0 ^= n;
        }
        for (int i = 1; i <= nums.length; i++) {
            if ((i & rightmostbit) != 0)
                xor1 ^= i;
            else
                xor0 ^= i;
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == xor0)
                return new int[]{xor0, xor1};
        }
        return new int[]{xor1, xor0};
    }
```
