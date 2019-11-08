# 804. Unique Morse Code Words

## 题目

给定一个字符串数组 `word[]` ，每个字符串只包含小写字母。摩斯电码将每个字母转换成对应的码字，不考虑字母之间的间隔时，不同的字符串可能转换成同一个摩斯电码码文。求将所有字符串转换成摩斯电码之后有多少种码文。

>International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to ".-", "b" maps to "-...", "c" maps to "-.-.", and so on.
>
>For convenience, the full table for the 26 letters of the English alphabet is given below:
>
>>[`".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."`]
>
>Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cba" can be written as `"-.-..--..."`, (which is the concatenation `"-.-."` + `"-..."` + `".-"`). We'll call such a concatenation, the transformation of a word.
>
>Return the number of different transformations among all words we have.
>
>**Example:**
>>Input: words = ["gin", "zen", "gig", "msg"]  
>>Output: 2  
>>Explanation:  
>>The transformation of each word is:  
>>`"gin" -> "--...-."`  
>>`"zen" -> "--...-."`  
>>`"gig" -> "--...--."`  
>>`"msg" -> "--...--."`  
>
>There are 2 different transformations, `"--...-."` and `"--...--."`.
>
>**Note:**
>
> - The length of words will be at most 100.
> - Each `words[i]` will have length in range `[1, 12]`.
> - `words[i]` will only consist of lowercase letters.

## 解法

用一个HashSet保存所有字符串转换成的码文。

时间复杂度O(S), 空间复杂度O(S)。S为数组长度。

```java
public int uniqueMorseRepresentations(String[] words) {
        String[] code = new String[]
        {".-","-...","-.-.","-..",".","..-.","--.",
        "....","..",".---","-.-",".-..","--","-.",
        "---",".--.","--.-",".-.","...","-","..-",
        "...-",".--","-..-","-.--","--.."};
        HashSet<String> set = new HashSet<>();
        for (String word : words) {
            StringBuilder temp = new StringBuilder();
            for (char c : word.toCharArray())
                temp.append(code[c - 'a']);
            set.add(temp.toString());
        }
        return set.size();
    }
```
