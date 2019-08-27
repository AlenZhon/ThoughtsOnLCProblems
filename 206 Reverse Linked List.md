# 206. Reverse Linked List

## 题目

>Reverse a singly linked list.
>
>**Example:**
>
>>Input: 1->2->3->4->5->NULL  
>>Output: 5->4->3->2->1->NULL
>
>**Follow up:**
>
>A linked list can be reversed either iteratively or recursively. Could you implement both?

## 解法

### 1. Iterative

把当前元素的next指针指向前一个元素。由于是单向链表，故需要提前将前一个链表元素用prev记录下来。考虑到边界值，可将prev初始值设为null，翻转后null即为链表的结尾。

时间复杂度O(n)，空间O(1)

```java
public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        return prev;
    }
```

### 2. Recursive

这个解法比较有意思。假设从第k个元素之后的链表已经翻转完毕，而当前在第k个元素。即：

n_1 -> ... -> n_k -> n_{k+1} <- ... <- n_m

需要将n_{k+1} 的next指针指向n_k，所以：
`head.next.next = head;`

考虑到n_1翻转之后它需要指向null，否则会出现自环。

```java
public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode temp = reverseList(head.next);
        head.next.next = head; //nice one
        head.next = null;
        return temp;
    }
```
