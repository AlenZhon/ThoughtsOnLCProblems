# 23. Merge k Sorted Lists

## 题目

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

>**Example:**
>
>**Input:**
>>[  
>>1->4->5,  
>>1->3->4,  
>>2->6  
>]  
>>**Output:** 1->1->2->3->4->4->5->6

## 解法

想了想排序，大佬们给出了优先级队列和分治归并的两种思路。

### 优先级队列

维护一个优先级队列，重写Comparator为升序排列。把所有链表的头结点放入优先级队列则已经排好，每次取出的必是目前最小的结点，再将取出结点的next结点放入队列，直到队列为空。思路清晰，考虑优先队列中的元素不超过 k 个，那么插入和删除的时间代价为 O(logk)，这里最多有 kn 个点，对于每个点都被插入删除各一次，故总的时间代价即渐进时间复杂度为 O(kn×logk)。渐进空间复杂度为O(k)。


```java
public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        PriorityQueue<ListNode> pq = new PriorityQueue<>(new Comparator<ListNode>(){
            @Override
            public int compare(ListNode o1, ListNode o2){
                return o1.val - o2.val;
            }
        });

        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        for (ListNode firstNode : lists){
            if (firstNode == null) continue;
            pq.add(firstNode);            
        }

        while (!pq.isEmpty()){
            ListNode temp = pq.poll();
            curr.next = temp;
            curr = curr.next;
            if (temp.next != null) pq.add(temp.next);
        }

        return dummy.next;
    }
```

其中定义优先级队列的时候可以用lambda表达式简化书写
```java
PriorityQueue<ListNode> pq = new PriorityQueue<>((l1, l2) ->(l1.val - l2.val));
```

### 分治合并

用到了归并排序的思路，假设总共有k个链表，那么渐进时间复杂度为O(knlogk)，空间复杂度用到了O(logk)层递归

```java
  public ListNode mergeKLists(ListNode[] lists) {
        if(lists==null || lists.length==0) return null;		
		return merge(lists,0,lists.length-1);
    }

    public ListNode merge(ListNode[] lists, int left, int right){
        if (left == right){ return lists[left];}
        int mid = left + (right - left) / 2;
        ListNode l1 = merge(lists, left, mid);
        ListNode l2 = merge(lists, mid + 1, right);
        return mergeTwoLists(l1, l2);
    }
    public ListNode mergeTwoLists(ListNode l1, ListNode l2){
        ListNode dummy = new ListNode(0), curr = dummy;
        while (l1 != null && l2 != null){
            if (l1.val < l2.val) {
                curr.next = l1;
                if (l1 != null) l1 = l1.next;
            } else {
                curr.next = l2;
                if (l2 != null) l2 = l2.next;
            }
            curr = curr.next;
        }
        curr.next = (l1 == null) ? l2 : l1;
        return dummy.next;
    }
```



