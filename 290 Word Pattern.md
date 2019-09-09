# 290. Word Pattern

## 题目

给定一个模式字符串`pattern`和一串由空格分隔的字符串`str`，判断两个字符串是否属于相同的文字模式。

>Given a `pattern` and a string `str`, find if str follows the same pattern.
>
>Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `str`.
>
>**Example 1:**
>
>>Input: pattern = "abba", str = "dog cat cat dog"  
>>Output: true
>
>**Example 2:**
>
>>Input:pattern = "abba", str = "dog cat cat fish"  
>>Output: false
>
>**Example 3:**
>
>>Input: pattern = "aaaa", str = "dog cat cat dog"  
>>Output: false
>
>**Example 4:**
>
>>Input: pattern = "abba", str = "dog dog dog dog"  
>>Output: false
>
>**Notes:**
>You may assume pattern contains only lowercase letters, and str contains lowercase letters that may be separated by a single space.

## 解法

整道题感觉是 *#205 Isomorphic Strings* 的升级版，当时是找`char`与`char`之间的映射关系，这里是找`char`和`String`的映射关系。

先按照直接的思路来。首先`String.split()`然后加一个HashMap一个一个比。如果`map`中已经有`key`则看已经存储的`value`是否`equals(s[i])`；如果没有`key`，就需要看`map`中是否已经有`s[i]`被映射到别的`key`上了。

```java
public boolean wordPattern(String pattern, String str) {
        String[] s = str.split(" ");
        if (s.length != pattern.length())
            return false;
        HashMap<Character, String> map = new HashMap<Character, String>();
        for (Integer i = 0; i< s.length; i++){
            char c = pattern.charAt(i);
            if(map.containsKey(c)){
                if(!map.get(c).equals(s[i]))
                    return false;
            }else{ //
                if(map.containsValue(s[i]))
                    return false;
                map.put(c, s[i]);
            }
        }
        return true;
    }
```

第一次submission就是没有加else中的`containsValue()`判断导致测试用例`"abba"，"dog dog dog dog"`过不了。

在讨论区中看到了一个老哥的[八行代码（奇技淫巧）](https://leetcode.com/problems/word-pattern/discuss/73402/8-lines-simple-Java)，贴在这里学习一下：

```java
public boolean wordPattern(String pattern, String str) {
    String[] words = str.split(" ");
    if (words.length != pattern.length())
        return false;
    Map index = new HashMap();
    for (Integer i=0; i<words.length; ++i)
        if (index.put(pattern.charAt(i), i) != index.put(words[i], i))
            return false;
    return true;
}
```

- 用了一个`HashMap<Object, Integer>`，键对应 letters和words，值对应它们最后一次出现时的索引。这样能避开时间复杂度O(n)的`containsValue()`，又不用新加一个`HashMap`。
- `HashMap`的`put()`方法是有返回值的。返回的是与`key`关联的旧值（此处即最后一次出现时的索引）；如果之前key没有关联旧值则返回`null`。
- 由于使用了包装类`Integer`做`HashMap`的`value`，可以直接使用 `!=` 运算符进行比较。大佬的原话是:

>... because there's no autoboxing-same-value-to-different-objects-problem anymore.

- 如果硬是要改成`int`则判断条件要变成如下形式，因为`int`在`HashMap`里会被自动打包成包装类( autoboxing )：

```java
if (!Objects.equals(map.put(pattern.charAt(i), i), map.put(s[i], i))) return false;
```

## Notes

尝试过在大佬的解法中只把`Integer`它改成`int`，会在测试用例较长（`"ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccdd"，"s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s s t t"`）报错。

因为JVM有一个Integer Cache Behavior，当出现以下类之一的两个实例（可能由autoboxing得到），如果它们的primitive value相等，使用`==`运算符将始终相等：

- `Boolean`
- `Byte`
- `Character` from **`\u0000`** to **`\u007f`** (7f is 127 in decimal)
- `Short`and `Integer` and `Long` from -128 to 127

回到刚才的测试用例。用例中最后两个字母`<d,t>`的下标分别是128 129，超过了Caching的范围。所以比较`index.put(pattern.charAt(i), i) != index.put(words[i], i)`使用的是两个Integer的reference进行比较，返回false而非我们期望返回的true。
