# 374. Guess Number Higher or Lower

## 题目

猜数字，给定初始范围`[1, n]`的整数。调用API `int guess(int num)`，如果目标数字大于猜的数字则返回1，小于猜的数字返回-1，猜中了返回0。要求猜中数字。

>We are playing the Guess Game. The game is as follows:
>
>I pick a number from 1 to n. You have to guess which number I picked.
>
>Every time you guess wrong, I'll tell you whether the number is higher or lower.
>
>You call a `pre-defined` API `guess(int num)` which returns 3 possible results (-1, 1, or 0):
>
> - -1 : My number is lower
> - 1 : My number is higher
> - 0 : Congrats! You got it!
>
>**Example :**
>
>>Input: n = 10, pick = 6  
>>Output: 6

## 解法

二分查找秒了。时间复杂度O(`log_2 n`)空间复杂度O(1)。

```java
public int guessNumber(int n) {
        int left = 1, right =n, mid = left + (right - left) /2;
        while (guess(mid) != 0) {
            if (guess(mid) == 1) left = mid + 1;
            else if (guess(mid) == -1 ) right = mid -1;
            mid = left + (right - left) / 2;
        }
        return mid;
    }
```

Solution还提了一个三分查找？ 时间复杂度O(log_3 n) 空间复杂度O(1)。

```java
public int guessNumber(int n) {
        int low = 1;
        int high = n;
        while (low <= high) {
            int mid1 = low + (high - low) / 3;
            int mid2 = high - (high - low) / 3;
            int res1 = guess(mid1);
            int res2 = guess(mid2);
            if (res1 == 0)
                return mid1;
            if (res2 == 0)
                return mid2;
            else if (res1 < 0)
                high = mid1 - 1;
            else if (res2 > 0)
                low = mid2 + 1;
            else {
                low = mid1 + 1;
                high = mid2 - 1;
            }
        }
        return -1;
    }
```

然而在最坏情况下，三分查找所需要的比较次数比二分查找的多，所以经常使用二分查找。
