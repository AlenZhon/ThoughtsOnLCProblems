# 168. Excel Sheet Column Title

## 题目描述

>给定一个正整数n，要求返回它在excel表中对应列的名称。
>
>>示例 1:
>>
>>输入: 1  
>>输出: "A"
>>
>>示例 2:
>>
>>输入: 28  
>>输出: "AB"
>>
>>示例 3:
>>
>>输入: 701
>>输出: "ZY"

## 怎么解的

相当于一个26进制，主要关注一个从[0,25]->[1,26]的映射问题。比如`78=3*26+0`正常写为C0，但在excel中需要写成`BZ`即2*26+26。可以碰到结尾是0 的形式再做判断，但每次取余操作时减1也可解决这个问题。

```java
 public String convertToTitle(int n) {
        StringBuffer s = new StringBuffer();
        while (n> 0) {
            n--;
            s.insert(0,(char)(n % 26 + 65));
            n = n / 26;
        }
        return s.toString();
    }
```

## Notes

- String不可变没有append() insert() reverse()方法，所以需要StringBuffer。
- A的ASCII值是65（十六进制的41），小写a是97（十六进制的61）
