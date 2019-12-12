# 1200. Minimum Absolute Difference

## 题目

给定一个数组`arr`，数组元素各不相同。两两元素组成一对，找到所有差值绝对值最小的元素对。

>Given an array of distinct integers arr, find all pairs of elements with the minimum absolute difference of any two elements.
>
>Return a list of pairs in ascending order(with respect to pairs), each pair [a, b] follows
>
> - a, b are from arr
> - a < b
> - b - a equals to the minimum absolute difference of any two elements in arr
>
>**Example 1:**
>
>>Input: arr = [4,2,1,3]  
>>Output: [[1,2],[2,3],[3,4]]  
>>Explanation: The minimum absolute difference is 1. List all pairs with difference equal to 1 in ascending order.
>
>**Example 2:**
>
>>Input: arr = [1,3,6,10,15]  
>>Output: [[1,3]]  
>
>**Example 3:**
>
>>Input: arr = [3,8,-10,23,19,-4,-14,27]  
>>Output: [[-14,-10],[19,23],[23,27]]
>
>**Constraints:**
>
> - 2 <= arr.length <= 10^5
> - -10^6 <= arr[i] <= 10^6

## 解法

排序，排序之后最小差值只会出现在相邻两个元素之间。

```java
public List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr);
        List<List<Integer>> ret = new ArrayList();
        int minDiff = Integer.MAX_VALUE;
        for (int i = 1; i< arr.length; i++){
            if (arr[i] - arr[i - 1] < minDiff){
                minDiff = arr[i] - arr[i - 1];
                ret.clear();
            } else if (arr[i] - arr[i - 1] > minDiff) continue;
            ArrayList<Integer> temp = new ArrayList<>();
            temp.add(arr[i-1]);
            temp.add(arr[i]);
            ret.add(temp);
        }
        return ret;
    }
```
