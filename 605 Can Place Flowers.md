# 605. Can Place Flowers

## 题目

有一个二值数列代表一个长形的花盆，1代表此处有花，0代表此处没花。要求两朵花不能相邻。先需要向花盆中加入n朵花，判断能否成功放入。

>Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.
>
>Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.
>
>Example 1:
>
>>Input: flowerbed = [1,0,0,0,1], n = 1  
>>Output: True
>
>Example 2:
>
>>Input: flowerbed = [1,0,0,0,1], n = 2  
>>Output: False
>
>**Note:**
>
> - The input array won't violate no-adjacent-flowers rule.
> - The input array size is in the range of [1, 20000].
> - n is a non-negative integer which won't exceed the input array size.

## 解法

时间复杂度O(n)，空间O(1)。一次遍历，判断是否是连续3个0（或是开头两个0 或结尾两个0），如果是则置1，增加count计数。如果count >= n 则能够放入。

```java
public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i-1] == 0) && (i == flowerbed.length - 1 || flowerbed[i+1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
            if (count >= n) return true;
        }
        return false;
    }
```

如果不改变数列中的数，可以计算连续0的个数。就是开头和结尾连续0的情况要多加考虑。分成了全是0，开头或结尾的连续0，夹在中间的连续0三种情况。

```java
public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 0) {
                int j = i + 1;
                while (j < flowerbed.length && flowerbed[j] == 0) j++;
                int zeros = j - i; // number of continuous 0s
                if (i == 0 && j == flowerbed.length) {
                    count+= (zeros % 2 == 0) ? zeros / 2 : zeros / 2 + 1;
                    return count>=n;
                }
                if (i == 0 || j == flowerbed.length)
                    count+= zeros / 2;
                else
                    count+= (zeros % 2 == 0) ? zeros / 2 - 1: zeros / 2;
                i = j;
            }
            if (count>=n) return true;
        }
        return false;
    }
```
