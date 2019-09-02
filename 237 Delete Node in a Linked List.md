# 237. Delete Node in a Linked List

## 题目

>Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
>
>Given linked list -- `head = [4,5,1,9]`
>
>**Example 1:**
>
>>Input: head = [4,5,1,9], node = 5  
>>Output: [4,1,9]  
>>Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
>
>**Example 2:**
>
>>Input: head = [4,5,1,9], node = 1  
>>Output: [4,5,9]  
>>Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.
>
>**Note:**
>
> - The linked list will have at least two elements.
> - All of the nodes' values will be unique.
> - The given node will not be the tail and it will always be a valid node of the linked list.
> - Do not return anything from your function.

## 想法

非常奇怪的一题，而且它的备注也多到了4条。备注中给了一些限制条件： 链表长度至少为2，链表节点的值各不相同，需要删除的节点必存在且不会是链表的末尾。

要求在不给出链表首地址，只给出需要删除的节点的情况下删除该节点。因为只有node节点可以操作，且没有指向node前驱的指针，所以不能用常规的方法。

由于该节点不会是链表末尾，也就是说 `node.next != null` 恒为真，这也提示可能要用`node.next.next`，那么就容易想到了（但我还是初见杀555）。

```java
node.val = node.next.val;
node.next = node.next.next;
```

因垂丝汀。
