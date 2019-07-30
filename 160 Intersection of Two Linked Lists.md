# 160 Intersection of Two Linked Lists

## 题目描述

给定两个单链表，找出两个表相交的第一个节点，若不相交返回null。
>Write a program to find the node at which the intersection of two singly linked lists begins.
>
>>Example 1:
>>
>>**Input:** intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3  
>>**Output:** Reference of the node with value = 8  
>>**Input Explanation:** The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
>>
>>Example 2:
>>
>>**Input:** intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1  
>>**Output:** Reference of the node with value = 2  
>>**Input Explanation:** The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
>>
>>Example 3:
>>
>>**Input:** intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2  
>>**Output:** null  
>>**Input Explanation:** From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
>
>Notes:
>
>- If the two linked lists have no intersection at all, return `null`.
>- The linked lists must retain their original structure after the function returns.
>- You may assume there are no cycles anywhere in the entire linked structure.
>- Your code should preferably run in O(n) time and use only O(1) memory.

## 怎么解的

先求两个链表各自长度，减去长度差使两者长度相等后逐个判断节点是否相交，如果都不相交则最后都为null。设两列表节点个数分别为a,b，计算长度必须有时间复杂度O(a)+O(b)，调整长度差和逐个判断的时间复杂度最多为O(max(a,b))。

```java
 public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        int lenA = 0, lenB = 0;
        ListNode temp = headA;
        while (temp != null) {
            lenA ++;
            temp = temp.next;
        }
        temp = headB;
        while (temp != null) {
            lenB ++;
            temp = temp.next;
        }

        temp = headA;
        ListNode temp2 = headB;
        if (lenA > lenB) {
            while (lenA > lenB) {
                temp = temp.next;
                lenA --;
            }
        } else {
            while (lenB > lenA) {
                temp2 =temp2.next;
                lenB --;
            }
        }
        while (temp != temp2) {
            temp = temp.next;
            temp2 = temp2.next;
        }
        return temp;
    }
```

评论区老哥给出了一种优雅的解决方法，贴在这里：

```java
 public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        /**
        定义两个指针, 第一轮让两个到达末尾的节点指向另一个链表的头部, 最后如果相遇则为交点(在第一轮移动中恰好抹除了长度差)
        两个指针等于移动了相同的距离, 有交点就返回, 无交点就是各走了两条指针的长度
        **/
        if(headA == null || headB == null) return null;
        ListNode pA = headA, pB = headB;
        // 在这里第一轮体现在pA和pB第一次到达尾部会移向另一链表的表头, 而第二轮体现在如果pA或pB相交就返回交点, 不相交最后就是null==null
        while(pA != pB) {
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
```

漂亮的地方在于他使用`pA = headB`和`pB = headA`，从而让两指针相遇时走了相同的距离，抹除了两个链表的长度差。时间复杂度和上面的做法是一样的。

没有看到retain original structure的要求，先人为构造一个环，再按照#142 的快慢指针做法来做。（一堆if else if 是很丑陋了）

```java
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB ==null) return null;
        ListNode temp = headB;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = headB;

        ListNode fast = headA, slow = headA;
        do {
            if (slow == temp)
                slow = temp.next;
            else
                slow = slow.next;
            if (fast == null || fast.next == null) {
                temp.next = null; //没有这句则提交时会显示破坏链表结构的错误
                return null;
            } else {
                if (fast == temp) fast = temp.next.next;
                else if (fast.next == temp) fast = temp.next;
                else fast = fast.next.next;
            }
        } while (slow != fast);

        slow = headA;
        while (slow != fast) {
            slow = slow.next;
            if (fast == temp) fast = temp.next;
            else fast = fast.next;
        }
        temp.next =null; //
        return slow;
    }
```
