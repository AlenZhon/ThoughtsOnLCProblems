# 1078. Occurrences After Bigram

## 题目

给定一些文字，和字符串 first 和 second，要求在文字中找到形如`"first second third"`的形式，并把所有 third 加入到答案中返回。

>Given words first and second, consider occurrences in some text of the form "first second third", where second comes immediately after first, and third comes immediately after second.
>
>For each such occurrence, add "third" to the answer, and return the answer.
>
>**Example 1:**
>
>>Input: text = `"alice is a good girl she is a  good student"`, first = `"a"`, second = `"good"`  
>>Output: `["girl","student"]`
>
>**Example 2:**
>
>>Input: text = `"we will we will rock you"`, first = `"we"`, second = `"will"`  
>>Output: `["we","rock"]`  
>
>**Note:**
>
> - `1 <= text.length <= 1000`
> - text consists of space separated words, where each word consists of lowercase English letters.
> - `1 <= first.length, second.length <= 10`
    `first` and `second` consist of lowercase English letters.

## 解法

无脑`split()`然后比较，再添加到`list`里面。(3ms)

```java
public String[] findOcurrences(String text, String first, String second) {
        String[] words = text.split("\\s+");
        List<String> ret = new LinkedList<String>();
        for (int i = 0; i< words.length - 2; i++){
            if (words[i].equals(first) && words[i+1].equals(second))
                ret.add(words[i+2]);
        }
        return ret.toArray(new String[ret.size()]);
    }
```

或者可以使用`indexOf()`在text中查找`first + " " + second+ " "`出现的位置（隐含`first`和`second`的中间只有一个空格的假设）。只需遍历一遍`text`即可。(0ms)

```java
public String[] findOcurrences(String text, String first, String second) {
        String match = first + " " + second + " ";
        List<String> ret = new ArrayList<>();
        int len = match.length(), index = text.indexOf(match);
        while (index != -1){
            if (index == 0 || text.charAt(index -1) == ' '){ //
                int start = index + len, end = start;
                while (end < text.length() && text.charAt(end) != ' ')
                    end++;
                ret.add(text.substring(start, end));
            }
            index = text.indexOf(match, index + 1);
        }
        return ret.toArray(new String[ret.size()]);
    }
```

其中`while`循环里的`if`语句防止了`index`之前不是空格，即`first`字符串只是`text`中某个词的子串。("aa good student"前面有a，这个student不能算)
