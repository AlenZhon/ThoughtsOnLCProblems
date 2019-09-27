# 496. Next Greater Element I

## 题目

两个整型数组`nums1, nums2`，前者的所有元素均在后者出现，且`nums2`的元素不重复。对于每个nums1的元素，找到它在`nums2`中右边第一个大于它的元素（不存在则返回-1）。

>You are given two arrays **(without duplicates)** `nums1` and `nums2` where `nums1`’s elements are subset of `nums2`. Find all the next greater numbers for `nums1`'s elements in the corresponding places of `nums2`.
>
>`The Next Greater Number` of a number **x** in `nums1` is the first greater number to its right in `nums2`. If it does not exist, output `-1` for this number.
>
>**Example 1:**
>
>>Input: nums1 = [4,1,2], nums2 = [1,3,4,2].  
>>Output: [-1,3,-1]  
>>Explanation:  
>>For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.  
>>For number 1 in the first array, the next greater number for it in the second array is 3.  
>>For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
>
>**Example 2:**
>
>>Input: nums1 = [2,4], nums2 = [1,2,3,4].  
>>Output: [3,-1]  
>>Explanation:  
>>For number 2 in the first array, the next greater number for it in the second array is 3.  
>>For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
>
>**Note:**
>
> - All elements in `nums1` and `nums2` are unique.
> - The length of both `nums1` and `nums2` would not exceed 1000.

## 解法

使用一个HashMap存放`nums2`的元素和存放位置，这样查找起来更快一些。（问题：如果`nums2`元素很多而`nums1`元素很少是不是就不太值得了）

```java
public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] res = new int[nums1.length];
        HashMap<Integer, Integer> map = new HashMap<Integer,Integer>();
        for (int i = 0; i< nums2.length; i++)
            map.put(nums2[i], i);
        for (int i = 0; i< nums1.length; i++) {
            int n = map.get(nums1[i]), j =n;
            while (j < nums2.length && nums2[j] <= nums2[n])
                j++;
            res[i] = (j == nums2.length) ? -1 : nums2[j];
        }
        return res;
    }
```

讨论区给出了[一种解法](https://leetcode.com/problems/next-greater-element-i/discuss/97595/Java-10-lines-linear-time-complexity-O(n)-with-explanation)。用了一个`stack`遍历存储nums2的元素，当新元素大于栈顶元素时表示该新元素即为`the Next Greater Element`，出栈直到新元素小于栈顶元素。

```java
public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Map<Integer, Integer> map = new HashMap<>(); // map from x to next greater element of x
        Stack<Integer> stack = new Stack<>();
        for (int num : nums) {
            while (!stack.isEmpty() && stack.peek() < num)
                map.put(stack.pop(), num);
            stack.push(num);
        }
        for (int i = 0; i < findNums.length; i++)
            findNums[i] = map.getOrDefault(findNums[i], -1);
        return findNums;
    }
```
