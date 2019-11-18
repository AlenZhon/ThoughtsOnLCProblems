# 933. Number of Recent Calls

## 题目

构造一个类，实现`ping(int t)`方法，要求该方法能记录下之前3000 milliseconds之内即`[t- 3000, t]`时间内`ping`的次数。

>Write a class RecentCounter to count recent requests.
>
>It has only one method: ping(int t), where t represents some time in milliseconds.
>
>Return the number of pings that have been made from 3000 milliseconds ago until now.
>
>Any ping with time in [t - 3000, t] will count, including the current ping.
>
>It is guaranteed that every call to ping uses a strictly larger value of t than before.
>
>**Example 1:**
>
>>Input: inputs = ["RecentCounter","ping","ping","ping","ping"], inputs = [[],[1],[100],[3001],[3002]]  
>>Output: [null,1,2,3,3]
>
>**Note:**
>
> - Each test case will have at most 10000 calls to ping.
> - Each test case will call ping with strictly increasing values of t.
> - Each call to ping will have `1 <= t <= 10^9`.

## 解法

一个滑动窗口内的元素计数，用了队列完成入队出队的操作。

```java
class RecentCounter {
    private Queue<Integer> time;
    public RecentCounter() {
        time = new LinkedList();
    }

    public int ping(int t) {
        time.offer(t);
        while (time.peek() < t - 3000)
            time.poll();
        return time.size();
    }
}

```
