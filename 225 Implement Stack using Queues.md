# 225. Implement Stack using Queues

## 题目

使用队列queue实现一个栈的如下方法：`push()`, `pop()`, `peek()`, `empty()`。

>Implement the following operations of a stack using queues.
>
> - push(x) -- Push element x onto stack.
> - pop() -- Removes the element on top of the stack.
> - top() -- Get the top element.
> - empty() -- Return whether the stack is empty.
>
>**Example:**
>
>```java
>MyStack stack = new MyStack();
>
>stack.push(1);
>stack.push(2);  
>stack.top();   // returns 2
>stack.pop();   // returns 2
>stack.empty(); // returns false
>```
>
>**Notes:**
>
> - You must use only standard operations of a queue -- which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
> - Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
> - You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

## 解法

Java里`Queue`是一个接口，通常由`array`或`LinkedList`实现，这里用的链表。  
`Queue`还提供插入（`add()`, `offer()`）、取出（`remove()`, `poll()`）和检查(`element()`, `peek()`)操作，每个方法都存在两种形式：前者抛出异常，后者返回特殊值（null 或 false，具体取决于操作）。

使用了一个Queue和top变量，实现复杂度为O(1)的`push()`和O(n)的`pop()`。[Solution](https://leetcode.com/problems/implement-stack-using-queues/solution/)里也提供了不同的解法，比如`O(n) push(), O(1) pop()`

```java
class MyStack {

    private Queue<Integer> list = new LinkedList<Integer>();
    private int top;
    /** Initialize your data structure here. */
    public MyStack() {

    }

    /** Push element x onto stack. */
    public void push(int x) {
        list.add(x);
        top =x;
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        Integer temp = 0;
        while (list.peek() != top) {
            temp = list.peek();
            list.add(list.poll());
        }
        top = temp;
        return list.poll();
    }

    /** Get the top element. */
    public int top() {
        return top;
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return list.size() == 0;
    }
}
```

## Notes

相关的题目还可以看 *#155 Min Stack* 也是实现一个Stack类。
