# 500. Keyboard Row

## 题目

>Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.
>
>(an image of a `QWERTY` keyboard)
>
>**Example:**
>
>>Input: ["Hello", "Alaska", "Dad", "Peace"]  
>>Output: ["Alaska", "Dad"]
>
>**Note:**
>
> - You may use one character in the keyboard more than once.
> - You may assume the input string will only contain letters of alphabet.

给出一个字符串组成的数组。判断每个字符串是否能被美式键盘上的同一行字母打出。返回满足要求的所有字符串。

## 解法

题给的例子里有大写有小写，是不是还要按`shift / caps lock`的键才能打出来（笑）。

算了，在和HashMap比较的时候自己转换一下好了。

存储的时候使用的是`ArrayList`，最后转成`String[]`的方法是 `list.toArray(new String[list.size()])`

```java
public String[] findWords(String[] words) {
        String[] s = new String[]{"qwertyuiop","asdfghjkl","zxcvbnm"};
        List<String> ret = new ArrayList<String>();
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (int i = 0; i< s.length; i++)
            for (char c : s[i].toCharArray())
                map.put(c, i);
        for (String cur : words) {
            if (cur.length() == 0) continue;
            int row = map.get(Character.toLowerCase(cur.charAt(0)));
            for (int i = 0; i< cur.length(); i++)
                if (row != map.get(Character.toLowerCase(cur.charAt(i)))) {
                    row = -1; // raise a flag
                    break;
                }
            if (row != -1) ret.add(cur);
        }
        return ret.toArray(new String[ret.size()]);
    }
```
