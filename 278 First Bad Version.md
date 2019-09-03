# 278. First Bad Version

## 题目

在软件版本迭代开发的过程中，某一个版本出了问题，导致之后所有的迭代版本都有问题。假设版本号为[1,2,3,...,n]，找出第一个出问题的版本号。
>You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.
>
>Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.
>
>You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.
>
>**Example:**
>
>Given `n = 5`, and `version = 4` is the first bad version.
>
>>call `isBadVersion(3)` -> false  
>>call `isBadVersion(5)` -> true  
>>call `isBadVersion(4)` -> true  
>
>Then 4 is the first bad version.

## 解法

二分查找的典型例题。

```java
 public int firstBadVersion(int n) {
        int left = 1 ,  right = n;
        while (left < right) {
            int mid = left + (right - left) /2;
            if (isBadVersion(mid))
                right = mid;
            else
                left = mid + 1;
        }
        return left;
    }
```

注意两个小点：

### 1. left和right的更新选取

本题中，初始值`left = 1, right = n`，`mid`是两者的中间值取整。那么：  
  如果`isBasVersion(mid) == true`，则表示mid之后的版本都是坏版本舍弃不用，但`mid`不能被确定是第一个坏版本，所以`right = mid;`  
  如果`isBasVersion(mid) == true`，则表示mid以及mid之前的版本都是正确的，不用再检查。有`left = mid +1;`

快速检查写好的二分查找是否正确，可以用一个size =2的输入。
>Here is a helpful tip to quickly prove the correctness of your binary search algorithm during an interview. We just need to test an input of size 2. Check if it reduces the search space to a single element (which must be the answer) for both of the scenarios above. If not, your algorithm will never terminate.

### 2. Overflow Bug

避免在(left + right) / 2可能造成的数据溢出，更新`mid`一般使用`mid = left + (right - left) / 2;`
