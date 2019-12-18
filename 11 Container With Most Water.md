# 11. Container With Most Water

## 题目

用一个数组表示竖线的长度，竖线底端在x轴上且垂直，相邻竖线相距1个单位长度。找到这些竖线中任意两根与x轴所能围成的最大面积。

>Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
>
>Note: You may not slant the container and n is at least 2.
>
>The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`. In this case, the max area of water (blue section) the container can contain is 49.
>
>Example:
>
>>Input: [1,8,6,2,5,4,8,3,7]  
>>Output: 49

## 解法

既要考虑宽度，也要考虑竖线的高度。  
two pointers。 从首尾出发向中间寻找。

```java
public int maxArea(int[] height) {
        int left = 0, right = height.length - 1, volume = 0;
        while (left < right){
            int newVolume = Math.min(height[left], height[right]) * (right - left);
            if (volume < newVolume) volume = newVolume;
            if (height[left] < height[right])
                left++;
            else
                right--;
        }
        return volume;
    }
```

时间复杂度O(n) (2ms)
