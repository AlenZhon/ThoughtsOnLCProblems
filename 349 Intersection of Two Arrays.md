# 349. Intersection of Two Arrays

## 题目

给出两个数组，求出两个数组中均出现的元素。要求重复出现只计入一次。

>Given two arrays, write a function to compute their intersection.
>
>**Example 1:**
>
>>Input: nums1 = [1,2,2,1], nums2 = [2,2]  
>>Output: [2]
>
>**Example 2:**
>
>>Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
>>Output: [9,4]
>
>**Note:**
>
> - Each element in the result must be unique.
> - The result can be in any order.

## 解法

既然重复出现的元素只能算一次，自然想到Set。先把一个数组存到Set里，遍历另一个数组如果有相同元素就加到一个ArrayList中。

最后`ArrayList`不知道怎么转化成`int[]`，面向百度搜了一下，说用到了1.8的stream()功能。运行时间爆炸（runtime :36ms）

```java
public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<Integer>();
        for (int i :nums1) set.add(i);
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int j : nums2) {
            if (set.contains(j)) {
                list.add(j);
                set.remove(j);
            }
        }
        return list.stream().mapToInt(Integer::valueOf).toArray();
    }
```

Solution中给出的另一个解法调用了Set 内置的retainAll函数计算intersection。

```java
 public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set1 = new HashSet<Integer>();
        for (Integer n : nums1) set1.add(n);
        HashSet<Integer> set2 = new HashSet<Integer>();
        for (Integer n : nums2) set2.add(n);

        set1.retainAll(set2);

        int [] output = new int[set1.size()];
        int idx = 0;
        for (int s : set1) output[idx++] = s;
        return output;
    }
```

还有个老哥去Facebook面试被问这道题，要求时间复杂度为O(n)，空间复杂度O(1)（除了存储intersection的用量之外）。不过两个数组已经排序。

```java
public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1); // assume sorted
        Arrays.sort(nums2); // assume sorted

        int[] intersections = new int[nums1.length];

        int i1 = 0, i2 = 0, j=0;
        while (i1<nums1.length && i2<nums2.length) {
            int val1 = nums1[i1];
            int val2 = nums2[i2];

            if (val1 == val2) {
                intersections[j++]=val1;
                while (i1<nums1.length && val1 == nums1[i1]) i1++;
                while (i2<nums2.length && val2 == nums2[i2]) i2++;
            }
            if (val2 > val1)
                while(i1<nums1.length && val1 == nums1[i1]) i1++;
            else
                while(i2<nums2.length && val2 == nums2[i2]) i2++;

        }
        return Arrays.copyOf(intersections,j);
}
```
