# 67 Add Binary

## 题目描述

给定两个以非空字符串形式表示的二进制数。要求以字符串形式返回两二进制数之和。

>Example 1:
>
>>Input: a = "11", b = "1"  
>>Output: "100"
>
>Example 2:
>
>>Input: a = "1010", b = "1011"  
>>Output: "10101"

## 怎么解的

也就是从两字符串结尾按位相加。  
用到了StringBuilder存储需要返回的结果，方便每一位的append操作。  
最后把进位（如果是1）加到StringBuilder中，然后反序并转化成字符串。

```java
 public String addBinary(String a, String b) {
        int i = a.length()-1, j = b.length()-1;
        int temp_a, temp_b, sum, carry = 0;
        StringBuilder s = new StringBuilder();
        while ( i >= 0 || j >= 0 ) {
            temp_a = (i>=0) ? a.charAt(i)-'0' : 0;
            temp_b = (j>=0) ? b.charAt(j)-'0' : 0;
            sum = temp_a + temp_b + carry;
            s.append(sum%2);
            carry = sum / 2;
            i-=1;
            j-=1;
        }
        if (carry == 1) {s.append(carry);}
        return s.reverse().toString();
}
```

submit显示消耗时间2ms，64%。  
在discussion中看到有人不用`append()`和最后的`reverse()`，而是对每一位使用`insert(0,sum%2)`。这样最后就省去了`reverse()`。
