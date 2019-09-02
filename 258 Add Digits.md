# 258. Add Digits

## 题目

给一个非负整数，将它各位数字相加得到一新的数，再将该数各位数字相加，直到相加结果为个位数。输出该个位数。

>Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.
>
>**Example:**
>
>>Input: 38  
>Output: 2  
>>Explanation: The process is like: `3 + 8 = 11, 1 + 1 = 2.`  Since 2 has only one digit, return it.
>
>**Follow up:**  
>Could you do it without any loop/recursion in O(1) runtime?

## 解法

一看这个提示就知道肯定是有通项公式了。穷举前30个数发现以9为循环，那肯定与模9余数有关了。

```java
public int addDigits(int num) {
        if (num ==0) return 0;
        return (num %9 ==0) ? 9 : num % 9;
    }
```

可以用一行写完：

```java
return (num-1)%9 +1;
```

## Notes

*#168 Excel Sheet Column Title* 也有余数从[0,25]映射为[1,26]的操作。
