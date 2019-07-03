# 2 Add Two Numbers

## 题目描述

输入： 两个数342+465分别用链表形式存储每一位（从个位起） （2-> 4-> 3） （5->6->4）

输出： 两数之和807， 也由链表形式输出 （7->0->8）

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
**/

```

## 解题思路

设置一个ListNode和对应的引用，再设置一个临时进位temp

注意判断条件和边界条件
