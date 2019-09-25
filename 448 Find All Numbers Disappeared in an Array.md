# 448. Find All Numbers Disappeared in an Array

## 题目

有一个长度为n的整数数组，其中每个元素都在`[1, n]`的范围之内，并且有些元素重复出现。找出`[1, n]`范围内不在数组中的整数。

>Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.
>
>Find all the elements of [1, n] inclusive that do not appear in this array.
>
>Could you do it **without extra space and in O(n) runtime**? You may assume the returned list does not count as extra space.
>
>**Example:**
>
>>Input:
>>[4,3,2,7,8,2,3,1]
>>
>>Output:
>>[5,6]

## 解法

如果不要求`without extra space`可以构造一个下标数组`new int[nums.length]`每遍历一个元素就在对应下标加一，最后把保持为0的下标对应元素加入到列表中。

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        if (nums.length == 0) return res;
        int[] index = new int[nums.length];
        for (int i = 0 ; i<nums.length; i++)
            index[nums[i] - 1] = 1;
        for (int i = 0 ; i< index.length; i++)
            if (index[i] == 0) res.add(i+1);
        return res;
    }
```

这也提示我们这一题的关键在于数组的元素和它的下标有很强的关系。数组元素是`[1, n]`，而数组的下标是`[0, n-1]`。

如果不引入新的存储空间，怎样在原数组中标出已经遍历的下标呢？ 答案可以是取相反数，即`nums[nums[i] -1] = -nums[nums[i]-1]`。最后将保持为整数的下标对应元素加入到列表中。

```java
public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        if (nums.length == 0) return res;
        for (int i = 0 ; i< nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] >= 0) nums[index] = - nums[index];
        }
        for (int i = 0 ; i< nums.length; i++)
            if (nums[i] > 0) res.add(i+1);
        return res;
    }
```
