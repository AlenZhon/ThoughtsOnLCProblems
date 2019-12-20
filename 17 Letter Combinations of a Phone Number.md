# 17. Letter Combinations of a Phone Number

## 题目

给定一个字符串只包含`[2-9]`的数字，按照手机九键键盘的映射关系，按顺序按下所有数字能得到许多种字符串结果，返回所有结果。

>Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.
>
>A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
>
>**Example:**
>
>>Input: "23"  
>>Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
>
>**Note:**
>
>>Although the above answer is in lexicographical order, your answer could be in any order you want.

## 解法

构造一个数字到字母映射的关系，用char[8][]存储。

然后就逐个数字进行添加。

```java
public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList();

        if (digits.length() == 0) return ans;
        char[][] map = new char[8][];
        map[0] = "abc".toCharArray();
        map[1] = "def".toCharArray();
        map[2] = "ghi".toCharArray();
        map[3] = "jkl".toCharArray();
        map[4] = "mno".toCharArray();
        map[5] = "pqrs".toCharArray();
        map[6] = "tuv".toCharArray();
        map[7] = "wxyz".toCharArray();

        ans.add("");
        for (char c : digits.toCharArray())
            ans = helper(ans, map[c - '2']);
        return ans;
    }
    private List<String> helper(List<String> list, char[] chars){
        List<String> ret = new ArrayList();
        for (String s : list)
            for (char c : chars)
                ret.add(s + c);
        return ret;
    }
```
