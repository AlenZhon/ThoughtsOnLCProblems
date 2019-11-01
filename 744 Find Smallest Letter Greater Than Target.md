# 744. Find Smallest Letter Greater Than Target

## 题目

给出一个有序的char[]，元素均为小写字母。给定target，在数组中找到大于target且ASCII最小的字符。

此外，字符顺序形成一个环，例如 `target = z and letters = [a, b]`， 需要返回`a`。

>Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.
>
>Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.
>
>**Examples:**
>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "a"  
>>Output: "c"
>>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "c"  
>>Output: "f"
>>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "d"  
>>Output: "f"
>>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "g"  
>>Output: "j"
>>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "j"  
>>Output: "c"
>>
>>Input:  
>>letters = ["c", "f", "j"]
>>target = "k"  
>>Output: "c"
>
>**Note:**
>
> - letters has a length in range [2, 10000].
> - letters consists of lowercase letters, and contains at least 2 unique letters.
> - target is a lowercase letter.

## 解法

遍历。时间复杂度O(n)， 空间O(1).

```java
public char nextGreatestLetter(char[] letters, char target) {
        if (target >= letters[letters.length - 1]) return letters[0];
        int i = 0;
        while (letters[i] <= target)
            i++;
        return letters[i];
    }
```

由于是有序，也可以用二分查找。
