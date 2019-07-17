# 83. Remove Duplicates from Sorted List

## 题目描述

给定一有序元素组成的链表，要求将链表中重复的元素删除。

Given a sorted linked list, delete all duplicates such that each element appear only once.

>Example 1:  
>>Input: 1->1->2  
>>Output: 1->2  
>
>Example 2:  
>>Input: 1->1->2->3->3  
>>Output: 1->2->3

## 怎么解的

判断this节点和this.next节点元素是否重复，若重复则跳过next节点，否则将this指向next节点。

时间复杂度O(n),空间复杂度O(1)。

```java
 public ListNode deleteDuplicates(ListNode head) {
        ListNode l = head;
        while (l != null && l.next != null) {
            if (l.val == l.next.val) {
                l.next = l.next.next;
            } else {
                l = l.next;
            }
        }
        return head;
    }
```
