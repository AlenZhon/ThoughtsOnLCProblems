# 728. Self Dividing Numbers

## 题目

>A self-dividing number is a number that is divisible by every digit it contains.
>
>For example, 128 is a self-dividing number because `128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0`.
>
>Also, a self-dividing number is not allowed to contain the digit zero.
>
>Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.
>
>**Example 1:**
>
>>Input:  
left = 1, right = 22  
Output: `[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]`  
>
>**Note:**
>>The boundaries of each input argument are `1 <= left <= right <= 10000`.

## 解法

Straight-forward. 对每一个区间内的数每一位分解判断。

```java
    public List<Integer> selfDividingNumbers(int left, int right) {
        List<Integer> ret = new LinkedList<>();
        for (int x = left ; x <= right; x++)
            if (flag(x)) ret.add(x);
        return ret;
    }

    private boolean flag(int n) {
        for (int i = n; i> 0; i /= 10)
            if (i % 10 == 0 || n % (i % 10) != 0) return false;
        return true;
    }
```

时间复杂度O(n). n 为区间长度。
