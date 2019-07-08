# 21 Merge Two Sorted Lists

## 题目描述

输入两个已经排好序的链表，要求将它们合并成一个有序链表后输出。

>Example:  
>>Input: 1->2->4, 1->3->4  
>>Output: 1->1->2->3->4->4

## 我的想法

两个指针分别指向l1 ,l2两个链表的表头，比较两者大小，小的写入新链表直到结束。 时间复杂度为O(n)。

实际coding的时候犯了两个傻：

- 还按照val值重新创建新链表`p.next = new ListNode(temp_val)`，而不是`p.next = l1`或`p.next = l2`
- 上一条直接导致判断结束的条件没有想清楚，当某一链表(如l1)到结尾时直接让'p.next = l2'即可把之后所有的元素合并到新链表中。

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode L = new ListNode(0), p = L;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                p.next = l1;
                if (l1 != null) {l1 = l1.next;}
            } else {
                p.next = l2;
                if (l2 != null) {l2 = l2.next;}
            }
            p = p.next;
        }
        p.next = (l1 == null) ? l2 : l1;
        return L.next;
    }
}
```
