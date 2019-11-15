# 917. Reverse Only Letters

## 题目

>Given a string S, return the "reversed" string where all characters that are not a letter stay in the same place, and all letters reverse their positions.
>
>**Example 1:**
>
>>Input: "ab-cd"  
>>Output: "dc-ba"  
>
>**Example 2:**
>
>>Input: "a-bC-dEf-ghIj"  
>>Output: "j-Ih-gfE-dCba"  
>
>**Example 3:**
>
>>Input: "Test1ng-Leet=code-Q!"  
>>Output: "Qedo1ct-eeLg=ntse-T!"
>
>**Note:**
>
> - `S.length <= 100`
> - `33 <= S[i].ASCIIcode <= 122`
> - S doesn't contain `\` or `"`

## 解法

two-pointers。时间复杂度O(N)，空间复杂度O(N)。

```java
public String reverseOnlyLetters(String S) {
        char[] c = S.toCharArray();
        for (int i = 0, j = c.length - 1; i < j;){
            while (i < j && !Character.isLetter(c[i])) i++;
            while (i < j && !Character.isLetter(c[j])) j--;

            char temp = c[i];
            c[i++] = c[j];
            c[j--] = temp;
        }
        return new String(c);
    }
```
