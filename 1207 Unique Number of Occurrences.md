# 1207. Unique Number of Occurrences

## 题目

给定一个数组，统计数组中各元素的重复次数。如果各元素的重复次数各不相同则返回true，否则返回false。

>Given an array of integers `arr`, write a function that returns `true` if and only if the number of occurrences of each value in the array is unique.
>
>**Example 1:**
>
>>Input: arr = [1,2,2,1,1,3]  
>>Output: true  
>>Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.
>
>**Example 2:**
>
>>Input: arr = [1,2]  
>>Output: false  
>
>**Example 3:**
>
>>Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]  
>>Output: true
>
>**Constraints:**
>
> - 1 <= arr.length <= 1000
> - -1000 <= arr[i] <= 1000

## 解法

自信题目。哈希表或者自己`new int[2001]`即可。

```java
public boolean uniqueOccurrences(int[] arr) {
        int[] occur = new int[2001];
        for (int a : arr)
            occur[a + 1000]++;
        int[] numOccur = new int[1000];
        for (int occurrence : occur){
            if (occurrence == 0) continue;
            if (numOccur[occurrence] > 0) return false;
            else numOccur[occurrence]++;
        }
        return true;
    }
```

实际上，元素的重复次数上限可进一步降低为`arr.length`。构造resArr用于存放重复次数的出现频次。

```java
public boolean uniqueOccurrences(int[] arr) {
        int[] resArr = new int[arr.length];
        // -1000 - 0 - 1000
        int[] countArr = new int[2001];
        for (int num : arr) {
            int count = countArr[num + 1000]++;
            if (count > 0)
                resArr[count]--;
            resArr[count + 1]++;
        }
        for (int a : resArr) {
            if (a > 1) {
                return false;
            }
        }
        return true;
    }
```
