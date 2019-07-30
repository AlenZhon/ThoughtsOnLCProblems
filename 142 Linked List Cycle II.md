# 142 Linked List Cycle II

## 题目描述

给定一个链表，判断该链表是否有自指向环，并返回入环的第一个节点。  
最好能使用O(1)空间复杂度。
>Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
>
>To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.
>
>Note: Do not modify the linked list.
>
>>Example 1:
>>
>>Input: head = [3,2,0,-4], pos = 1  
>>Output: tail connects to node index 1  
>>Explanation: There is a cycle in the linked list, where tail connects to the second node.  
>>
>>Example 2:
>>
>>Input: head = [1,2], pos = 0  
>>Output: tail connects to node index 0  
>>Explanation: There is a cycle in the linked list, where tail connects to the first node.  
>>
>>Example 3:
>>
>>Input: head = [1], pos = -1  
>>Output: no cycle  
>>Explanation: There is no cycle in the linked list.  

## 怎么解的

也是使用的快慢指针方法，并且用到了一个性质。

**性质：** 设入环节点为A，快慢指针相遇节点为B，那么可以用一个从起点开始的新指针temp和从节点B开始的慢指针slow同步走，两者相遇的地方必然是入环的第一个节点A。

**证明：**  
设起点到入环节点A的距离为a，A到相遇节点的距离为x，环的长度为b。由于相遇时快指针fast肯定比慢指针slow多走了m个环(m>=1)的距离，则距离关系有：

2 (a + x) = a + mb + x

化简即： a = mb - x

将temp设为从起点开始和slow同步走，则temp 经过a到达节点A， slow也经过 a = mb-x，加上之前走的x恰好走完一个环的长度，故slow也到达入环节点A。

```java
public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) return null;
        ListNode  slow = head, fast = head;
        do {
            if (fast ==null || fast.next == null) return null;
            slow = slow.next;
            fast = fast.next.next;
        } while (fast != slow);
        ListNode temp = head;
        while (temp != slow) {
            temp = temp.next;
            slow = slow.next;
        }
        return temp;
}
```

用do while循环是让初始时相等的快慢指针错开，不然这个循环就废了。

由于快慢指针相遇时slow == fast，若精简变量可将temp取消，让slow重新指向开头，fast速度变为1。
