# 561. Array Partition I

## 题目

>Given an array of **2n** integers, your task is to group these integers into n pairs of integer, say `(a1, b1), (a2, b2), ..., (an, bn)` which makes sum of `min(ai, bi)` for all i from 1 to n as large as possible.
>
>Example 1:
>
>>Input: `[1,4,3,2]`  
>>Output: `4`  
>>Explanation: n is 2, and the maximum sum of pairs is `4 = min(1, 2) + min(3, 4)`.
>
>**Note:**
>
> - n is a positive integer, which is in the range of `[1, 10000]`.
> - All the integers in the array will be in the range of `[-10000, 10000]`.

## 解法

最笨的方法： 先排个序再相隔累加。排序时间复杂度O(nlogn)，累加O(n)，空间O(1)。

```java
public int arrayPairSum(int[] nums) {
        int sum =0;
        Arrays.sort(nums);
        for (int i =0; i< nums.length; i+=2)
            sum+= nums[i];
        return sum;
    }
```

以空间换时间？构造一个`new int[20001]`的哈希数组，每隔一个数就累加一次。时间复杂度O(n)，空间复杂度O(1)

```java
public int arrayPairSum(int[] nums) {
        int[] hash = new int[20001];
        for (int num : nums)
            hash[num + 10000]++;
        int sum = 0, toAdd = 1;
        for (int i= 0; i< 20001;)
            if (hash[i] > 0) {
                if (toAdd == 1) sum+= i- 10000;
                hash[i]--;
                toAdd = ~toAdd;
            } else {
                i++;
            }
        return sum;
    }
```
