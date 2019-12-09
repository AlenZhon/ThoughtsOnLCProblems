# 1122. Relative Sort Array

## 题目

给定两个数组`arr1` `arr2`，其中后者的数组元素不重复，且后者所有的元素都在前者中出现。将前者的数组元素按照如下规则排序：先排在`arr2`中出现的元素，再排未出现的元素。出现的元素按照元素在`arr2`中出现的先后顺序排序，未出现的元素按照从小到大的顺序排序。

>Given two arrays `arr1` and `arr2`, the elements of `arr2` are distinct, and all elements in `arr2` are also in `arr1`.
>
>Sort the elements of `arr1` such that the relative ordering of items in `arr1` are the same as in `arr2`.  Elements that don't appear in `arr2` should be placed at the end of `arr1` in ascending order.
>
>**Example 1:**
>
>>Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]  
>>Output: [2,2,2,1,4,3,3,9,6,7,19]
>
>**Constraints:**
>
> - arr1.length, arr2.length <= 1000
> - 0 <= arr1[i], arr2[i] <= 1000
> - Each arr2[i] is distinct.
> - Each arr2[i] is in arr1.

## 解法

由于约束条件里限制了数值范围在[0, 1000]，很容易得到如下的解法：

- new 一个`int[1001]`存储`arr1`中数组元素的出现个数。
- 遍历`arr2`，按照刚才的`int[1001]`更新arr1里的值。

```java
public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int[] dict = new int[1001];
        for (int a : arr1)
            dict[a]++;
        int count = 0;
        for (int a2 : arr2){
            while (dict[a2]-- > 0)
                arr1[count++] = a2;
        }
        for (int i = 0; i<= 1000; i++)
            while (dict[i]-- > 0)
                arr1[count++] = i;
        return arr1;
    }
```

如果寻求更通用的方法，把`int[1001]`改成`HashMap`。
