# 234. Palindrome Linked List

## 题目

给定一个链表，判断链表是否回文。

>Given a singly linked list, determine if it is a palindrome.
>
>**Example 1:**
>
>>Input: 1->2  
>>Output: false
>
>**Example 2:**
>
>>Input: 1->2->2->1  
>>Output: true
>
>**Follow up:**  
>Could you do it in O(n) time and O(1) space?

## 解法

由于有复杂度的限制，所以引入新的数据结构不适合。

先用 *#141 #142*的快慢指针解法求出链表最中间节点（分奇偶）；再用 *#206* 的迭代方法将链表的前半段翻转。最后，从中间节点向首尾遍历，比较每个节点的值是否相等。

```java
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        // now the slow pointer points at the middle of the list
        ListNode prev = null, curr = head;
        while (prev != slow) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        if (fast == null) prev = prev.next; // odd case
        while (curr != null) {
            if (curr.val != prev.val) return false;
            curr = curr.next;
            prev = prev.next;
        }
        return true;
    }
```

## Notes

综合了 *#141 #142 #206* 好几道链表题目的解法。
