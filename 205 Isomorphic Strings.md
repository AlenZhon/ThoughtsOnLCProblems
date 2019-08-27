# 205. Isomorphic Strings

## 题目

>Given two strings s and t, determine if they are isomorphic.
>
>Two strings are isomorphic if the characters in s can be replaced to get t.
>
>All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.
>
>>**Example 1:**
>>
>>Input: s = "egg", t = "add"  
>>Output: true
>>
>>**Example 2:**
>>
>>Input: s = "foo", t = "bar"  
>>Output: false
>>
>>**Example 3:**
>>
>>Input: s = "paper", t = "title"  
>>Output: true
>
>**Note:**  
>You may assume both s and t have the same length.

## 怎么解的

用了两个hashMap的菜鸡想法。把两个字符串里所有字符的映射关系全部记录下来。

```java
public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) return false;
        char[] s1 = s.toCharArray();
        char[] t1 = t.toCharArray();
        HashMap<Character, Character> mapst = new HashMap<Character, Character>();
        HashMap<Character, Character> mapts = new HashMap<Character, Character>();
        for (int i = 0; i< s1.length; i++) {
            if (!mapst.containsKey(s1[i])) mapst.put(s1[i], t1[i]);
            if (!mapts.containsKey(t1[i])) mapts.put(t1[i], s1[i]);
            if (mapst.get(s1[i]) != t1[i] || mapts.get(t1[i]) != s1[i]) return false;
        }
        return true;
    }
```

一开始想不用char[]直接用String，在运行时间上直接用String的`charAt()`为15ms，先`toCharArray()`再用数组做的运行时间是11ms。  
旁边坐着的阿斌说不用哈希表也可以。

发现可以从字符出现的模式，而非字符之间的映射关系进行考虑。如egg和add可映射为122，paper和title可映射为12134，而foo映射为122，bar为123故两者不是可替换的。

改成了这样，时间复杂度O(n)空间复杂度O(1)。字符集若是unicode可能预分配空间就要变多一些。

```java
  public boolean isIsomorphic(String s, String t) {
        int[] dict_s = new int[256];
        int[] dict_t = new int[256];
        for (int i=0; i< s.length(); i++) {
            if (dict_s[s.charAt(i)] != dict_t[t.charAt(i)]) return false;
            dict_s[s.charAt(i)] = i+1;
            dict_t[t.charAt(i)] = i+1;
        }
        return true;
    }
```

1ms的示例解法是这样的：

```java
 public boolean isIsomorphic(String s, String t) {
        char[] temp=new char[128];
        char[] temp1=new char[128];
        char[] S=s.toCharArray();
        char[] T=t.toCharArray();
        int length=s.length();
        for(int i=0;i<length;i++)
        {
            if(temp[S[i]]!='\0'||temp1[T[i]]!='\0')
            {
                if(temp1[T[i]]!=S[i])
                    return false;
            }else{
                temp[S[i]]=T[i];
                temp1[T[i]]=S[i];
            }
        }
        return true;
    }
```
