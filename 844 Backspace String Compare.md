# 844. Backspace String Compare

## 题目

在空的文本编辑器分别输入以下两个字符串，其中字符串只包含小写字母和 `#`（代表在文本编辑器中键入退格键）。请判断输入完成后两个文本编辑器上的字符是否相同。

>Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.
>
>**Example 1:**
>
>>Input: S = "ab#c", T = "ad#c"  
>>Output: true  
>>Explanation: Both S and T become "ac".
>
>**Example 2:**
>
>>Input: S = "ab##", T = "c#d#"  
>>Output: true  
>>Explanation: Both S and T become "".
>
>**Example 3:**
>
>>Input: S = "a##c", T = "#a#c"  
>>Output: true  
>>Explanation: Both S and T become "c".
>
>**Example 4:**
>
>>Input: S = "a#c", T = "b"  
>>Output: false  
>>Explanation: S becomes "c" while T becomes "b".
>
>**Note:**
>
> - 1 <= S.length <= 200
> - 1 <= T.length <= 200
> - S and T only contain lowercase letters and '#' characters.
>
>**Follow up:**
>
> - Can you solve it in O(N) time and O(1) space?

## 解法

straight-forword。用栈的结构生成字符串井号退格相当于pop()。注意在pop()的时候检查是否为空（不排除对着空的编辑器按退格键的操作）。时间复杂度和空间复杂度均为O(N1 + N2)。分别是两个字符串的长度。

```java
public boolean backspaceCompare(String S, String T) {
        return helper(S).equals(helper(T));
    }
    private String helper(String st){
        Stack<Character> ans = new Stack();
        for (char c : st.toCharArray()){
            if (c != '#')
                ans.push(c);
            else if (!ans.isEmpty())
                ans.pop();
        }
        return String.valueOf(ans);
    }
```

如果考虑O(N)时间O(1)空间的解法。首先是想到用同一个`int[26]`去存储字母出现的次数，但是不引入新的数据结构无法记下连续`#`号对应着的字母。

？怎么办？

two-pointers从后向前，就可以知道我们见到了多少个退格键，从而直接跳过。

```java
public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1, j = T.length() - 1;
        while (i>=0 || j>=0) {
            int iskip = 0, jskip = 0;
            while (i >= 0){
                if (S.charAt(i) == '#') {iskip++; i--;}
                else if (iskip > 0) {iskip--; i--;}
                else break;
            }
            while (j >= 0){
                if (T.charAt(j) == '#') {jskip++; j--;}
                else if (jskip > 0) {jskip--; j--;}
                else break;
            }
            if (i>= 0 && j >=0 && S.charAt(i) != T.charAt(j)) return false;
            if ((i>=0) != (j>=0)) return false;
            i--; j--;
        }
        return true;
    }
```
