# 1114. Print in Order

## 题目

有一个`Foo`类将被传给三个线程，分别执行类中的三个方法。现在要求三个方法依次调用。

>Suppose we have a class:
>
>```java
>public class Foo {
>  public void first() { print("first"); }
>  public void second() { print("second"); }
>  public void third() { print("third"); }
>}
>```
>
>The same instance of Foo will be passed to three different threads. Thread A will call `first()`, thread B will call `second()`, and thread C will call `third()`. Design a mechanism and modify the program to ensure that `second()` is executed after `first()`, and `third()` is executed after `second()`.
>
>**Example 1:**
>
>>Input: [1,2,3]  
>>Output: "firstsecondthird"  
>>Explanation: There are three threads being fired asynchronously. The input [1,2,3] means thread A calls first(), thread B calls second(), and thread C calls third(). "firstsecondthird" is the correct output.
>
>**Example 2:**
>
>>Input: [1,3,2]  
>>Output: "firstsecondthird"  
>>Explanation: The input [1,3,2] means thread A calls first(), thread B calls third(), and thread C calls second(). "firstsecondthird" is the correct output.
>
>**Note:**
>
>>We do not know how the threads will be scheduled in the operating system, even though the numbers in the input seems to imply the ordering. The input format you see is mainly to ensure our tests' comprehensiveness.

## 解法

第一次做多线程的题目。一开始查到的是可以使用`volatile`关键字声明变量，使得不同线程在运行时能够从JVM的主内存中及时更新变量的最新值。`volatile` 变量具有 `synchronized` 的可见性特性，但是不具备原子特性。

只能在有限的一些情形下使用 `volatile` 变量替代锁。要使 `volatile` 变量提供理想的线程安全，必须同时满足下面两个条件：

- 对变量的写操作不依赖于当前值。
- 该变量没有包含在具有其他变量的不变式中。

实际上，这些条件表明，可以被写入 volatile 变量的这些有效值独立于任何程序的状态，包括变量的当前状态。根据题意，即使我们用volatile修饰变量count，print语句也不会受影响，满足这两个条件。

```java
private volatile int count;
    public Foo() {
        count = 1;
    }

    public void first(Runnable printFirst) throws InterruptedException {
        while (count != 1);
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        count = 2;
    }

    public void second(Runnable printSecond) throws InterruptedException {
        while (count != 2);
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        count = 3;
    }

    public void third(Runnable printThird) throws InterruptedException {
        while (count != 3);
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
        count = 4;
    }
```

AtomicInteger 原子整数类型，是Integer类型的线程安全原子类，可以在多线程中以原子的方式更新int值。查看源码，可以发现类中关于value的声明就是用了volatile关键字。基于AtomicInteger类的实现：

```java
 private AtomicInteger jobDone = new AtomicInteger(0);
    public Foo() {

    }

    public void first(Runnable printFirst) throws InterruptedException {
        while (jobDone.get() != 0);
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        jobDone.incrementAndGet();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        while (jobDone.get() != 1);
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        jobDone.incrementAndGet();
    }

    public void third(Runnable printThird) throws InterruptedException {
        while (jobDone.get() != 2);
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
    }
```

### What is 原子操作

Wikipedia里这么写的：

>In database systems, atomicity is one of the ACID (Atomicity, Consistency, Isolation, Durability) transaction properties. An atomic transaction is an indivisible and irreducible series of database operations such that either all occur, or nothing occurs.

简单来说就是不可分割性？我的理解：由于它们是不可分割的，一个线程无法在另一个线程执行此原子操作时跳过此操作，实现线程安全。
