# 771. Jewels and Stones

## 题目

两个字符串分别表示哪些石头是珠宝和你手上的石头。计算你手上这堆石头里有几件珠宝。

>You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.
>
>The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".
>
>Example 1:
>
>>Input: J = "aA", S = "aAAbbbb"  
>>Output: 3
>
>Example 2:
>
>>Input: J = "z", S = "ZZ"  
>>Output: 0
>
>Note:
>
> - S and J will consist of letters and have length at most 50.
> - The characters in J are distinct.

## 解法

先把珠宝的种类存下来，再一个个比较？

```java
public int numJewelsInStones(String J, String S) {
        boolean[] jewels = new boolean[52];
        for (char c :J.toCharArray()) {
            if (c >= 'a' && c <= 'z') jewels[c - 'a'] = true;
            if (c >= 'A' && c <= 'Z') jewels[c - 'A' + 26] = true;
        }
        int count = 0;
        for (char c : S.toCharArray()) {
            if (c >= 'a' && c <= 'z' && jewels[c - 'a']) count++;
            if (c >= 'A' && c <= 'Z' && jewels[c - 'A' + 26]) count++;
        }
        return count;
    }
```

因为题目限定了大小写字母所以用了一个`boolean[]`，时间复杂度和两个字符串的长度有关，空间复杂度O(1)。用HashSet也可以，更具有鲁棒性。

0ms的解法用的是遍历S字符串，`J.indexOf(S.charAt(i))`去判断是不是jewel。但其中转换成Int的操作有点骚（char就够了吧）。

```java
public int numJewelsInStones(String J, String S) {
       int count = 0;
        for(int i = 0; i < S.length(); i++) {
            int stone = (int)S.charAt(i);
            if(J.indexOf(stone) != -1)
                count ++;
        }
        return count;
    }
```
