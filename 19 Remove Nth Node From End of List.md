# 19. Remove Nth Node From End of List

## 题目

给定一个链表，将倒数第N个节点移除。返回移除后的链表。

>Given a linked list, remove the n-th node from the end of list and return its head.
>
>**Example:**
>
>>Given linked list: 1->2->3->4->5, and n = 2.
>>
>>After removing the second node from the end, the linked list becomes 1->2->3->5.
>
>**Note:**
>
>>Given n will always be valid.
>
>**Follow up:**
>
>>Could you do this in one pass?

## 解法

two-pointer大法好。将fast指针朝前移动n次，然后再同步移动。

注意移除链表首项的情况。

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode slow = head, fast = head;
        for (int i = 0; i < n; i++)
            fast = fast.next;
        while (fast.next != null){
            slow = slow.next;
            fast = fast.next;
        } // now slow.next is the node that should be deleted
        if (slow == head)
            head = slow.next;
        else
            slow.next = slow.next.next;
        return head;
    }
```
