# 155 Min Stack

## 题目描述

设计一个最小栈，支持push,pop,top以及获取栈中最小元素的操作，且操作所用时间为常数级。

>Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
>
> - push(x) -- Push element x onto stack.
> - pop() -- Removes the element on top of the stack.
> - top() -- Get the top element.
> - getMin() -- Retrieve the minimum element in the stack.
>
>Example:  
>MinStack minStack = new MinStack();  
>minStack.push(-2);  
>minStack.push(0);  
>minStack.push(-3);  
>minStack.getMin();   --> Returns -3.  
>minStack.pop();  
>minStack.top();      --> Returns 0.  
>minStack.getMin();   --> Returns -2.  

## 怎么解的

用了两个栈，一个stack正常存数据，一个minstack存最小值数据，这样minstack的栈顶元素始终是stack栈中的最小值。

```java
 class MinStack {

    private Stack<Integer> stack = new Stack<Integer>();
    private Stack<Integer> minstack = new Stack<Integer>();
    /** initialize your data structure here. */
    public MinStack() {

    }

    public void push(int x) {
        stack.push(x);
        if (minstack.isEmpty() || x <= minstack.peek())  //1
            minstack.push(x);
    }

    public void pop() {
        if (!minstack.isEmpty() && stack.peek().equals(minstack.peek()))  //2
            minstack.pop();
        stack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minstack.peek();
    }
}
```

Submission的运行时间是46ms，打败了差不多一半提交。

## Notes

- 注释1 `x<=minstack.peek()`的等号一定要加，如果不加则无法处理栈中有多个相同的最小元素的情况。
- 注释2 `stack.peek().equals(minstack.peek())`在这里比较的是两者的值是否相同。如果用`==`运算则是比较两者是否指向同一个内存空间。

## 其他解法

看到了有人只用了一个栈进行设计，加上一个Integer min变量。思路是：

1. 如果要push进来的元素小于等于当前的min，就先把当前的min也push进去。
2. 如果st.pop()与min相等，就`min = st.pop()`。相当于连续pop两次，且此时min即为pop之后当前栈内元素最小值。

```java
class MinStack {

   Stack<Integer> st = new Stack<Integer>();
   int min = Integer.MAX_VALUE;

   public MinStack() {

   }
   public void push(int x) {
     if (x <= min) {
       st.push(min);
       min = x;
     }
     st.push(x);
   }

   public void pop() {
     if (st.pop() == min)
       min = st.pop();
   }

   public int top() {
     return st.peek();
   }

   public int getMin() {
     return min;
   }
}
```

**Runtime:** 44 ms, faster than 99.99% of Java online submissions for Min Stack.  
**Memory Usage:** 40.4 MB, less than 31.09% of Java online submissions for Min Stack.
