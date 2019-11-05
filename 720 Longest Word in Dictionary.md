# 720. Longest Word in Dictionary

## 题目

一个String[]代表英语词典，某些单词可以用词典中其他字符串逐个字母添加得到，找到这些单词中最长的那个。如果最长单词有多个，则返回按照字母表顺序最靠前的单词（如示例2）。

>Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.
If there is no answer, return the empty string.
>
>**Example 1:**
>
>>Input:  
>>words = `["w","wo","wor","worl", "world"]`
>>Output: "world"  
>>Explanation:  
>>The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
>
>**Example 2:**
>
>>Input:  
>>words = `["a", "banana", "app", "appl", "ap", "apply", "apple"]`  
>>Output: "apple"  
>>Explanation:  
>>Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
>
>**Note:**
>
> - All the strings in the input will only contain lowercase letters.
> - The length of words will be in the range [1, 1000].
> - The length of words[i] will be in the range [1, 30].

## 解法

暴力写一版。先排序保证多个答案时按字母表顺序排列。然后检查字符串的`substring(0, k)`是否都在数组中（可以通过HashSet实现）。

维持满足条件的字符串长度ansLen，每个待检查的字符串提前判断，减少循环次数。

```java
public String longestWord(String[] words) {
        HashSet<String> set = new HashSet<String>();
        for (String word : words) set.add(word);
        Arrays.sort(words);
        int ansLen = -1, ansIndex = -1;
        for (int i = 0; i< words.length; i++){
            boolean flag = true;
            if (words[i].length() <= ansLen) continue;
            for (int k = 1; k < words[i].length(); k++)
                if (!set.contains(words[i].substring(0, k))) {
                    flag = false;
                    break;
                }
            if (flag) {
                ansIndex = i;
                ansLen = words[i].length();
            }
        }
        return ansIndex == -1 ? "" : words[ansIndex];
    }
```

时间复杂度 O(\sum wi ^2)，其中wi是每个字符串的长度。空间复杂度 O(\sum wi ^2)。

### Alternative Method (Using Trie + DFS)

介绍一种新的数据结构Trie， 字典树。字典树(主要用于存储字符串)查找速度主要和它的元素(字符串)的长度相关`[O(w)]`。 如果只考虑小写字母，那么字典树的每个节点最多可能有26个子节点。

> **Algorithm:** Put every word in a trie, then depth-first-search from the start of the trie, only searching nodes that ended a word. Every node found (except the root, which is a special case) then represents a word with all it's prefixes present. We take the best such word.
>
>**Complexity Analysis**
>
> - Time Complexity: `O(\sum w_i)`, where wiw_iwi​ is the length of words[i]. This is the complexity to build the trie and to search it.  
>If we used a BFS instead of a DFS, and ordered the children in an array, we could drop the need to check whether the candidate word at each node is better than the answer, by forcing that the last node visited will be the best answer.
> - Space Complexity: `O(\sum w_i)`, the space used by our trie.

```java
class Solution {
    public String longestWord(String[] words) {
        Trie trie = new Trie();
        int index = 0;
        for (String word: words) {
            trie.insert(word, ++index); //indexed by 1
        }
        trie.words = words;
        return trie.dfs();
    }
}

class Node {
    char c;
    HashMap<Character, Node> children = new HashMap();
    int end;
    public Node(char c) {
        this.c = c;
    }
}
class Trie {
    Node root;
    String[] words;
    public Trie() {
        root = new Node('0');
    }

    public void insert(String word, int index) {
        Node cur = root;
        for (char c : word.toCharArray()) {
            cur.children.putIfAbsent(c, new Node(c));
            cur = cur.children.get(c);
        }
        cur.end = index;
    }

    public String dfs() {
        String ans = "";
        Stack<Node> stack = new Stack();
        stack.push(root);
        while (!stack.isEmpty()) {
            Node node = stack.pop();
            if (node.end > 0 || node == root) {
                if (node != root) {
                    String word = words[node.end - 1];
                    if (word.length() > ans.length() ||
                       word.length() == ans.length() && word.compareTo(ans) < 0)
                        ans = word;
                }
                for (Node nei : node.children.values())
                    stack.push(nei);
            }
        }
        return ans;
    }
}
```
