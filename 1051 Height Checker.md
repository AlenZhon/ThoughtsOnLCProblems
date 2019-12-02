# 1051. Height Checker

## 题目

一队学生的身高用数组表示。让他们按从矮到高的顺序排列，最少需要让多少个学生移动位置？

>Students are asked to stand in non-decreasing order of heights for an annual photo.
>
>Return the minimum number of students not standing in the right positions.  (This is the number of students that must move in order for all students to be standing in non-decreasing order of height.)
>
>**Example 1:**
>
>>Input: [1,1,4,2,1,3]  
>>Output: 3  
>>Explanation:  
>>Students with heights 4, 3 and the last 1 are not standing in the right positions.
>
>**Note:**
>
> - 1 <= heights.length <= 100
> - 1 <= heights[i] <= 100

## 解法

拷贝一个数组之后排序，比较两个数组元素有几个不相同的。时间复杂度主要是排序的O(nlogn)

```java
public int heightChecker(int[] heights) {
        int[] h = Arrays.copyOf(heights, heights.length);
        Arrays.sort(h);
        int count =0;
        for (int i = 0; i< h.length; i++)
            if (h[i] != heights[i]) count++;
        return count;
    }
```

由于heights数组元素范围确定在`[1, 100]`而且是整数，可以用记录身高频次的方法来做。（有点取巧了）

```java
public int heightChecker(int[] heights) {
        int[] dict = new int[101];
        for (int height :heights)
            dict[height]++;
        int count = 0, nowIndex = 0;
        for (int i = 0; i< 101; i++) {
            for (int j = 0; j < dict[i]; j++)
                if (heights[nowIndex + j] != i) count++;
            nowIndex += dict[i];
        }
        return count;
    }
```
