# 20 Valid Parentheses

## 题目描述

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

>Example 1:  
>>Input: "()"  
>>Output: true
>
>Example 2:  
>>Input: "()[]{}"  
>>Output: true
>
>Example 3:  
>>Input: "(]"  
>>Output: false
>
>Example 4:
>>Input: "([)]"  
>>Output: false
>
>Example 5:  
>>Input: "{[]}"  
>>Output: true  

## 解法

如果parentheses 只有一种括号则：使用一个括号计数器即可，遍历所有字符，遇到左括号则计数器加一，右括号减一，若最后计数器不为0则 invalid。

考虑valid parentheses的子串，如Example2的三个括号，若划分为三个子串则子串也为valid。

可使用stack数据结构遍历并push每个左括号，当遇到一个右括号，则检查是否和栈顶元素配成一对，若是则pop。

## 想法

从单个括号的情况想起，所以一开始想用三个计数器变量分别计算大中小括号。看了看solution的方法，看来还是对数据结构的特点不熟悉。

.peek()方法会抛出EmptyStackException异常， 所以在使用之前先判断一下。

## 0ms 解法

```java
    public boolean isValid(String s) {
     int top = -1;
        char[] chs = s.toCharArray();
        for (int i = 0; i < chs.length; i++) {
            if (top < 0 || !isMatch(chs[top], chs[i])) {
                top++;
                chs[top] = chs[i];
            } else {
                top--;
            }
        }
        return top == -1;
    }

    private boolean isMatch(char c1, char c2){
        return ((c1 =='{' && c2 =='}') || (c1 =='[' && c2 ==']') || (c1 =='(' && c2 == ')'));
    }
```
