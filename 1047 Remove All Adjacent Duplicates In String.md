# 1047. Remove All Adjacent Duplicates In String

## 题目

给定一个字符串，如果其中两个相邻的字符相等，我们把这两个字符从字符串中去掉，叫做一次duplicates removal。重复此操作直到字符串中无法再进行duplicates removal，返回最后的字符串。答案保证是唯一的。

>Given a string S of lowercase letters, a duplicate removal consists of choosing two adjacent and equal letters, and removing them.
>
>We repeatedly make duplicate removals on S until we no longer can.
>
>Return the final string after all such duplicate removals have been made.  It is guaranteed the answer is unique.
>
>**Example 1:**
>
>>Input: "abbaca"  
>>Output: "ca"  
>>Explanation:  
>>For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
>
>**Note:**
>
> - 1 <= S.length <= 20000
> - S consists only of English lowercase letters.

## 解法

一开始觉得和之前的回文串有关系，但是题目的意思是需要迭代多次的。看了一眼题目提示，使用stack做。

于是直接撸了一个出来。考虑到栈的先进后出结构不太适合最后的append操作，所以从字符串结尾开始入栈。题目中明确说答案唯一，所以不会有其他答案。

```java
public String removeDuplicates(String S) {
        Stack<Character> stack = new Stack<>();
        for (int i = S.length() - 1; i >=0; i--)
            if (!stack.isEmpty() && stack.peek() == S.charAt(i))
                stack.pop();
            else
                stack.push(S.charAt(i));
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty())
            sb.append(stack.pop());
        return new String(sb);
    }
```

运行时间爆炸(51ms)。

Solution里有人用LinkedList取代`Stack。peek() pop() push()`方法对应的变成了`getLast() removeLast()和add()`方法。降低了一些运行时间。

最狠的解法是这样的：

```java
public String removeDuplicates(String S) {
        int length = S.length();
        char[] SArray = S.toCharArray();
        int i = 0;
        for(int j = 0; j < SArray.length; j++, i++){
            SArray[i] = SArray[j];

            if(i > 0 && SArray[i - 1] == SArray[i]){
                i -= 2;
            }
        }
        return new String(SArray, 0, i);
    }
```

当没检测到duplicates时，i和j同步增加。如果检测到duplicate，则i将回退，j继续增加，同时用j目前指向的元素覆盖i指向的元素，即把duplicate覆盖掉。
