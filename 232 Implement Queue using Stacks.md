# 232. Implement Queue using Stacks

## 题目

使用Stack实现一个队列的功能。

>Implement the following operations of a queue using stacks.
>
> - `push(x)` -- Push element x to the back of queue.
> - `pop()` -- Removes the element from in front of queue.
> - `peek()` -- Get the front element.
> - `empty()` -- Return whether the queue is empty.
>
>**Example:**
>
>```java
>MyQueue queue = new MyQueue();
>
>queue.push(1);
>queue.push(2);  
>queue.peek();  // returns 1
>queue.pop();   // returns 1
>queue.empty(); // returns false
>```
>
>**Notes:**
>
> - You must use only standard operations of a stack -- which means only `push to top`, `peek/pop from top`, `size`, and `is empty`operations are valid.
> - Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
> - You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

## 想法

和 *#225* 互为对应啊。
用两个Stack进行存储，在s1里push，在s2里pop和peek。当两个Stack都为空的时候表示空队列。push()的时间复杂度为O(1)，pop()的时间复杂度...[Solution](https://leetcode.com/problems/implement-queue-using-stacks/solution/)中用的说法叫做`Amortized O(1) per operation.`

```java
private Stack<Integer> s1 = new Stack<Integer>();
    private Stack<Integer> s2 = new Stack<Integer>();
    /** Initialize your data structure here. */
    public MyQueue() {
    }

    /** Push element x to the back of queue. */
    public void push(int x) {
        s1.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (s2.isEmpty())
            while (!s1.isEmpty())
                s2.push(s1.pop());
        return s2.pop();
    }

    /** Get the front element. */
    public int peek() {
        if (s2.isEmpty())
            while (!s1.isEmpty())
                s2.push(s1.pop());
        return s2.peek();
    }

    /** Returns whether the queue is empty. */
    public boolean empty() {
        return s1.isEmpty() && s2.isEmpty();
    }
```

## Notes

### Amortized Analysis

>Amortized analysis gives the average performance (over time) of each operation in the worst case. The basic idea is that a worst case operation can alter the state in such a way that the worst case cannot occur again for a long time, thus amortizing its cost.
>
>Consider this example where we start with an empty queue with the following sequence of operations applied:
>
>>push1,push2,…,push_n,pop1,pop2…,pop_n
>
>The worst case time complexity of a single pop operation is O(n)O(n)O(n). Since we have nnn pop operations, using the worst-case per operation analysis gives us a total of O(n^2) time.
>
>However, in a sequence of operations the worst case does not occur often in each operation - some operations may be cheap, some may be expensive. Therefore, a traditional worst-case per operation analysis can give overly pessimistic bound. For example, in a dynamic array only some inserts take a linear time, though others - a constant time.
>
>In the example above, the number of times pop operation can be called is limited by the number of push operations before it. Although a single pop operation could be expensive, it is expensive only once per n times (queue size), when s2 is empty and there is a need for data transfer between s1 and s2. Hence the total time complexity of the sequence is : `n (for push operations) + 2*n (for first pop operation) + n - 1 ( for pop operations)` which is O(2∗n).This gives `O(2n/2n) = O(1)` average time per operation.

### Implementation

评论区里有一个老哥面试时被问了[这个题目的实际应用](https://leetcode.com/problems/implement-queue-using-stacks/discuss/64284/Do-you-know-when-we-should-use-two-stacks-to-implement-a-queue)，答案是多线程中队列的读写分离。在多线程中，如果s2栈非空，则push()方法不会将整个队列锁住。
