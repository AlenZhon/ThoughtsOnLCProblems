# 796. Rotate String

## 题目

对字符串`A`的一个移位操作定义为将`A`最左边的第一个字符移动到最右边。现在给定字符串`A`, `B`，判断`A`是否能通过若干次移位操作变成`B`。

>We are given two strings, `A` and `B`.
>
>A shift on `A` consists of taking string `A` and moving the leftmost character to the rightmost position. For example, if `A = 'abcde'`, then it will be `'bcdea'` after one shift on `A`. Return True if and only if `A` can become `B` after some number of shifts on `A`.
>
>**Example 1:**
>>Input: `A = 'abcde', B = 'cdeab'`  
>>Output: true  
>
>**Example 2:**
>>Input: `A = 'abcde', B = 'abced'`  
>>Output: false
>
>Note:
>
> - `A` and `B` will have length at most 100.

## 解法

如果为真，那么B肯定是（A + A）的子串。同时需要判断A B的长度是否相等，否则会漏过`A ='a', B = 'aa'`的情况。时间复杂度O(n*n)，空间复杂度为O(n)。

```java
public boolean rotateString(String A, String B) {
        return A.length() == B.length() && (A + A).indexOf(B) != -1;
    }
```

## KMP (Knuth-Morris-Pratt) 算法

>用暴力算法匹配字符串过程中，我们会把两个字符串字符一一匹配，如果相同则匹配下一个字符，直到出现不相同的情况，此时我们会丢弃前面的匹配信息，模式串后移一格，循环进行，直到主串结束，或者出现匹配成功的情况。这种丢弃前面的匹配信息的方法，极大地降低了匹配效率。  
>而在KMP算法中，对于每一个模式串我们会事先计算出模式串的内部匹配信息，在匹配失败时最大的移动模式串，以减少匹配次数。  
>比如，在简单的一次匹配失败后，我们会想将模式串尽量的右移和主串进行匹配。右移的距离在KMP算法中是如此计算的：在已经匹配的模式串子串中，找出最长的相同的前缀和后缀，然后移动使它们重叠。  
在第一次匹配过程中
>T: a b a c a a b a c a b a c a b a a b b  
>W: a b a c a b  
>在 T[5] 与 W[5] 出现了不匹配，而 T[0]~T[4] 是匹配的，其中 T[0]~T[4] 就是上文中说的已经匹配的模式串子串，移动找出最长的相同的前缀和后缀并使他们重叠：  
T: a b a c a a b a c a b a c a b a a b b  
W: a b a c a b

```java
class Solution {
    public boolean rotateString(String A, String B) {
        int N = A.length();
        if (N != B.length()) return false;
        if (N == 0) return true;

        //Compute shift table
        int[] shifts = new int[N+1];
        Arrays.fill(shifts, 1);
        int left = -1;
        for (int right = 0; right < N; ++right) {
            while (left >= 0 && (B.charAt(left) != B.charAt(right)))
                left -= shifts[left];
            shifts[right + 1] = right - left++;
        }

        //Find match of B in A+A
        int matchLen = 0;
        for (char c: (A+A).toCharArray()) {
            while (matchLen >= 0 && B.charAt(matchLen) != c)
                matchLen -= shifts[matchLen];
            if (++matchLen == N) return true;
        }

        return false;
    }
}
```
