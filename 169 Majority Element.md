# 169. Majority Element

## 题目描述

给定一个数列，长度为n，找出数列中的众数。众数的定义为在数列中它出现次数大于 ⌊ n/2 ⌋。

>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.
>
>You may assume that the array is non-empty and the majority element always exist in the array.
>
>>Example 1:
>>
>>Input: [3,2,3]  
>>Output: 3
>>
>>Example 2:
>>
>>Input: [2,2,1,1,1,2,2]  
>>Output: 2

## 怎么解的

无脑用了个HashMap存<元素，出现次数>，然后比较出现次数的大小。时间复杂度是O(n)，空间复杂度也是。

```java
 public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0 ; i < nums.length; i++) {
            if (! map.containsKey(nums[i])) {
                map.put(nums[i], 1);
            } else {
                Integer count = map.get(nums[i]);
                map.put(nums[i], ++count);
            }
        }
        for (int i : map.keySet())
            if (map.get(i) > Math.floor(nums.length / 2))
                return i;
        return 0;
}
```

运行时间13ms（一顿操作猛如虎）。如何改进呢？

众数有个性质：如果对数列升序排序且众数存在，则众数一定出现在 ⌊ n/2 ⌋ （长度为奇数）或⌊ n/2 ⌋+1 （长度为偶数）的位置。  
根据这个性质，我们很容易就可以求得众数。时间复杂度由排序算法决定。Array.sort() 的时间复杂度是O(nlogn)。

```java
public int majorityElement(int[] nums) {
  Arrays.sort(nums);
  return nums[nums.length /2];
}
```

Solution中也有一个有趣的算法 Boyer-Moore Voting Algorithm。  
算法维护一个count变量和value变量，初始时将value设为数列的初值。之后遍历数列每看到一次value，count就加一，反之减一。当count重新为0时，此时指向的元素成为新的value。最后的value即为所求值。

这个算法把整个数列分成好几段，每一段中众数出现的次数和非众数出现次数相等，从而丢弃。时间复杂度O(n)

```java
 public int majorityElement(int[] nums) {
        int count = 0, value = 0;
        for (int n : nums) {
            if (count == 0) {
                value = n; count++;
            } else if (value == n)
                count++;
            else
                count--;
        }
        return value;
    }
```
