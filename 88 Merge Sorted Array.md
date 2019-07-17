# 88 Merge Sorted Array

## 题目描述

给定两个有序数组nums1和nums2,将nums2的所有元素插入到nums1中，使之依然有序。

两个数组中初始元素的个数分别为m和n，假设nums1中的初始数组空间足够（nums1不小于m+n个空间）。

>Example:
>
>Input:  
>nums1 = [1,2,3,0,0,0], m = 3  
>nums2 = [2,5,6],       n = 3
>
>Output: [1,2,2,3,5,6]

## 怎么解的

类似插入排序，设置m1和m2分别为两个数组的下标。滑动m1直到`nums1[m1]>nums2[m2]`，将m1到结尾的元素全体向后移。再把`nums2[m2]`插进去。submit后发现有好几个错。

- 一开始判断结尾用的是否等于0，原始数组里有0直接被打脸。
- 当m=0即nums1初始元素为0时，报ArrayIndexOutOfBound : -1。 解决方法：程序开始时提前判断这种情况。

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int mark1 = 0 ,mark2 = 0;
        if (m == 0) {   //提前判断m=0时情况
            mark2 = n;
            for (int i = 0; i< n; i++ ) { nums1[i] = nums2[i];}
        }
        while (mark2 < n) {
            int temp = m + mark2;
            while (nums1[mark1] <= nums2[mark2] && mark1 < temp) {    //滑动m1
                mark1++;
            }
            while (temp >= mark1 && temp >0) { //平移nums1中元素
                nums1[temp] = nums1[temp -1];
                temp--;
            }
            nums1[mark1] = nums2[mark2];
            mark2++;
        }
    }
```

debug结束，运行时间1ms，时间复杂度最坏时为O(mn)。0ms的解法从k=m+n-1开始反向考虑，时间复杂度O(m+n-1)。比较i,j指向的元素，大者放到k。第二个while处理(i== -1 && j>= 0)情况，类似如下示例(nums2中存在比nums1最小值还要小的元素)：
>nums1 = [2,5,6,0,0,0]  m = 3
>nums2 = [1,2,3] n = 3

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m -1;
        int j = n -1;
        int k = m + n -1;
        while(i >= 0 && j >= 0) {
            if(nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            }
            else {
                nums1[k] = nums2[j];
                j--;
            }
            k --;
        }
        while(j >= 0) {
            nums1[k] = nums2[j];
            k--;
            j--;
        }
    }
```

Discussion里有人把上面的代码压缩了行数：

```java
 public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m-1, j = n-1, k = m+n-1;
        while (i>=0 && j>=0) {
            nums1[k--] = nums1[i]>nums2[j]?nums1[i--]:nums2[j--];
        }
        while (i==-1 && j>=0)
            nums1[j] = nums2[j--];
    }
```
