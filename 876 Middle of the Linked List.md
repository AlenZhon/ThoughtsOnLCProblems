# 876. Middle of the Linked List

## 题目

一个链表，找到链表最中间的节点。如果链表有偶数个节点，返回第二个中间节点。

>Given a non-empty, singly linked list with head node head, return a middle node of linked list.
>
>If there are two middle nodes, return the second middle node.
>
>**Example 1:**
>
>>Input: [1,2,3,4,5]  
>>Output: Node 3 from this list (Serialization: [3,4,5])  
>>The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).  
>>Note that we returned a ListNode object ans, such that:  
>>`ans.val = 3, ans.next.val = 4,` `ans.next.next.val = 5,` and `ans.next.next.next = NULL`.
>
>**Example 2:**
>
>>Input: [1,2,3,4,5,6]  
>>Output: Node 4 from this list (Serialization: [4,5,6])  
>>Since the list has two middle nodes with values 3 and 4, we return the second one.  
>
>**Note:**
>
> - The number of nodes in the given list will be between 1 and 100.

## 解法

水题。快慢指针完事。时间复杂度O(n)，空间复杂度O(1).

```java
public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
```
