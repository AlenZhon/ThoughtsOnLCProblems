# 1002. Find Common Characters

## 题目

统计`String[] A`数组中在所有字符串均出现过的字母。如果该字母均出现过三次，那么在返回的答案中也要添加三个该字母。

>Given an array A of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (including duplicates).  For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.
>
>You may return the answer in any order.
>
>**Example 1:**
>
>>Input: ["bella","label","roller"]  
>>Output: ["e","l","l"]  
>
>**Example 2:**
>
>>Input: ["cool","lock","cook"]  
>>Output: ["c","o"]
>
>**Note:**
>
> - 1 <= A.length <= 100
> - 1 <= A[i].length <= 100
> - A[i][j] is a lowercase letter

## 解法

由于A的长度有约束，所以先无脑写一个char[A.length][26]的二维哈希数组。先把所有的字母频次统计一下，再慢慢比较找最小值。

时间复杂度`O(A.length * len)`，len是字符串中的字符个数。空间复杂度`O(A.length * 26)`

```java
public List<String> commonChars(String[] A) {
        int[][] count = new int[26][A.length];
        for (int i = 0; i< A.length; i++)
            for (int j = 0; j< A[i].length(); j++)
                count[A[i].charAt(j) - 'a'][i]++;
        List<String> ret = new ArrayList<String>();
        for (int i = 0; i< 26; i++){
            int minOccur = 100;
            for (int j = 0; j < A.length; j++)
                if(count[i][j] < minOccur) minOccur = count[i][j];
            for (int k = 0; k< minOccur; k++)
                ret.add("" + (char)(97 + i));
        }
        return ret;
    }
```

1ms的解法是这样的。只用了两个int[26]。

```java
    int[] arr = new int[26];
    public List<String> commonChars(String[] A) {
        List<String> list = new ArrayList<String>();
        if (A == null || A.length == 0) return list;
        int[] arr_ori = new int[26];
        for (char c : A[0].toCharArray()) {
            arr_ori[c - 'a']++;
        }
        for (int i = 1; i < A.length; i++) {
            countValid(A[i], arr_ori);
        }
        for (int i = 0; i < 26; i++) {
            if (arr_ori[i] != 0) {
                for (int j = 0; j < arr_ori[i]; j++) {
                    list.add((char)(i+'a') + "");
                }
            }
        }
        return list;
    }
    private void countValid(String str, int[] arr_ori) {
        for (char c : str.toCharArray()) {
            arr[c - 'a']++;
        }
        for (int i = 0; i < 26; i++) {
            if (arr_ori[i] != 0 && arr[i] != arr_ori[i]) {
                arr_ori[i] = Math.min(arr_ori[i], arr[i]);
            }
        }
        arr = new int[26];
    }
```
