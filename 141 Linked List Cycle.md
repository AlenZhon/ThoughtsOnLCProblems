# 141 Linked List Cycle

## 题目描述

给定一个链表，判断该链表是否有自指向循环。  
进阶要求：算法实现时使用O(1) 空间复杂度。
>Given a linked list, determine if it has a cycle in it.
>
>To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.
>
>Example 1:
>
>**Input:** head = [3,2,0,-4], pos = 1  
>**Output:** true  
>**Explanation:** There is a cycle in the linked list, where tail connects to the second node.
>
>Example 2:
>
>**Input:** head = [1,2], pos = 0  
>**Output:** true  
>**Explanation:** There is a cycle in the linked list, where tail connects to the first node.
>
>Example 3:
>
>**Input:** head = [1], pos = -1  
>**Output:** false  
>**Explanation:** There is no cycle in the linked list.
>
>**Follow up：** Can you solve it using O(1) (i.e. constant) memory?

## 怎么解的

首先是想把每个节点存起来，在遍历的过程中看是否出现了已经存起来的节点。用HashSet实现使得添加节点和查找结点的时间降为O(1)，总体时间复杂度为O(n)，空间复杂度O(n)。

```java
 public boolean hasCycle(ListNode head) {
        HashSet<ListNode> node = new HashSet<ListNode>();
        while (head != null) {
            if (node.contains(head)) {return true;}
            node.add(head);
            head = head.next;
        }
        return false;
    }
```

## 其他的解法

Solution给出了一种快慢指针的方法。快指针每次移动两个节点，慢指针每次移动一个节点。如果链表中有循环，那么快慢指针总会相遇；否则经过有限长时间，快慢指针均会指向链表尾部。

这种方法的时间复杂度在无循环情况下是O(n)，在有循环的情况下，由于两个指针的移动速度差是1，那么需要大约K次循环（K为循环中的节点个数）快指针才能与慢指针相遇。时间复杂度为O(1)。

```java
public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        ListNode slow = head, fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return false;
            }
            fast = fast.next.next;
            slow = slow.next;
        }
        return true;
```

要注意边界条件的判断：1)链表为空的提前return  2)快指针达到结尾`(fast ==null || fast.next == null)`

Submission 0ms，上一个方法用了4ms，有点真实。
