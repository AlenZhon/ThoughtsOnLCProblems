# 69 Sqrt(x)

## 题目描述

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

## 怎么解的

想到的是二分查找，但提交就发现了Wrong Answer，一看是if条件判断写的是`middle*middle <=x` ，左式溢出了Integer的数值范围。看讨论改成了`middle <= x/middle`。

边界条件的0也没有考虑周全，需要一开始就做判断。

```java
public int mySqrt(int x) {
        if (x == 0) { return 0;}
        int left =1, right =x;
        while (left < right) {
            int middle =(left + right) /2;
            if (middle <= x / middle && (middle +1) > x/ (middle + 1)) {
                return middle;
            } else if (middle > x / middle) {
                right = middle -1;
            } else {
                left = middle +1;
            }
        }
        return left;
}
```

## Notes

- 避免数值越界可使用 `middle`和`x/middle`做比较判断。
- 边界条件需要提前考虑清楚。
- 在讨论里看到了一种牛顿迭代法寻找开方数，贴在这里。

```java
public int mySqrt(int x) {
    if (x == 0) return 0;
    long i = x;
    while(i > x / i)  
      i = (i + x / i) / 2;
    return (int)i;
}
```
