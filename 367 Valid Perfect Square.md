# 367. Valid Perfect Square

## 题目

给定一个正整数，判断它是否是完全平方数。

>Given a positive integer `num`, write a function which returns True if num is a perfect square else False.
>
>**Note: Do not** use any built-in library function such as `sqrt`.
>
>**Example 1:**
>
>>Input: 16  
>>Output: true  
>
>**Example 2:**
>
>>Input: 14  
>>Output: false

## 解法

Integer范围内 最大的完全平方数是`46340* 46340 = 2147395600` 。

牛顿迭代法秒了。

```java
int i = num;
while (i > num /i) {
  i = (i + num / i) /2;
}
return i * i == num;
```

要不就用一个for 往上找。

```java
for (int i = 1; i < num / i; i++)
  if (i *i == num) return true;
return false;
```

或者二分查找。

## Notes

*#69 sqrt(x)* 里用到了牛顿迭代法快速求开方。
