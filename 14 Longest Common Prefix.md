# 14 Longest Common Prefix

## 题目描述

给定一个字符串数组`String[] strs`， 输出字符串数组各元素的最长的相同前缀。如果没有则输出空字符串。

示例：
>Example 1:  
>>**Input:** ["flower","flow","flight"]  
>>**Output:** "fl"
>
>Example 2:  
>>**Input:** ["dog","racecar","car"]  
>>**Output:** ""  
>>**Explanation:** There is no common prefix among the input strings.

## 我的解法

和Solution中的Approach2相似，按照每个字符串的每一位比较。若循环到某一数组元素的结尾或查到不一样的字母，则返回当前已经比对过的字符串。

时间复杂度为O(m*n), m为strs包含的元素个数，n为共有字母的个数。最差情况即为strs中所有元素均相同。常数空间复杂度。

## 其他解法

1. Divide & Conquer  
2. Binary Search

## 进一步拓展

>Given a set of keys S = [S_1,S_2 ,..., S_n], find the longest common prefix among a string q and S. This LCP query will be called frequently.

We could optimize LCP queries by storing the set of keys S in a Trie. For more information about Trie, please see this article Implement a trie (Prefix trie). In a Trie, each node descending from the root represents a common prefix of some keys. But we need to find the longest common prefix of a string q and all key strings. This means that we have to find the deepest path from the root, which satisfies the following conditions:

- it is prefix of query string q
    each node along the path must contain only one child element. Otherwise the found path will not be a common prefix among all strings.
- the path doesn't comprise of nodes which are marked as end of key. Otherwise the path couldn't be a prefix a of key which is shorter than itself.
