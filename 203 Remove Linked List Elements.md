# 203. Remove Linked List Elements

## 题目

给定一个链表和*val*，移除链表中所有与*val*相等的元素。

>Remove all elements from a linked list of integers that have value *val*.
>
>**Example:**
>
>**Input:**  1->2->6->3->4->5->6, val = 6  
>**Output:** 1->2->3->4->5

## 怎么写的

因为给的数据结构是单向链表，所以就判断`p.next.val`是否与*val*相等。

```java
 public ListNode removeElements(ListNode head, int val) {
        while (head != null && head.val == val) {
            head = head.next;
        }
        ListNode p = head;
        while (p != null) {
            if (p.next != null && p.next.val == val) {
                p.next = p.next.next;
            } else {
                p = p.next;
            }
        }
        return head;
    }
```

写这小十行代码错了两次。。。没有考虑`head == null`和`head.val == val`的情况，所以一开始根本没有写第一个`while`（我好菜啊.jpg）

突然想起来还可以用dummy head的方法处理上述情况。dummy head 的方法在#21 也使用过。

```java
public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode p = dummy;
        while (p != null) {
            if (p.next != null && p.next.val == val) {
                p.next = p.next.next;
            } else {
                p = p.next;
            }
        }
        return dummy.next;
    }
```
