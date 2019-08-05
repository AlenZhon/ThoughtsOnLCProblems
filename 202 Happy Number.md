# 202. Happy Number

## 题目要求

>Write an algorithm to determine if a number is "happy".
>
>A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.
>
>>**Example:**
>>
>>**Input:** 19  
>>**Output:** true  
>>**Explanation:**
>>1^2 + 9^2 = 82  
>>8^2 + 2^2 = 68  
>>6^2 + 8^2 = 100  
>>1^2 + 0^2 + 0^2 = 1

## 怎么写的

没想到有什么技巧，先按着思路来。分解每一位相加作比较，如果是1就`return true`同时维护一个`HashSet`存储之前所有的加和结果，如果`contains(sum)`就`return false`。

```java
public boolean isHappy(int n) {
        int sum = 0;
        HashSet<Integer> ans = new HashSet<Integer>();
        while (!ans.contains(n)){
            ans.add(n);
            while (n>=1) {
                sum = sum + (n%10)*(n%10);
                n /= 10;
            }
            if (sum == 1) return true;
            n = sum;
            sum = 0;
        }
        return false;
    }
```

Submit上去发现Runtime(2ms 60.15%)和Memory Usage(33.8MB 5.18%)都全面落后？

## 其他大胆的想法

运行时间0ms和1ms的代表性解法都是限定了外层循环次数，分别限定到7次和10次。在Discussion里[All you need to know about testing happy number!](https://leetcode.com/problems/happy-number/discuss/56918/all-you-need-to-know-about-testing-happy-number)通过枚举加推理的方式给出了一些证明。

同时，有个老哥提出了[另一个想法](https://leetcode.com/problems/happy-number/discuss/56917/My-solution-in-C(-O(1)-space-and-no-magic-math-property-involved-))，使用Floyd Cycle Detection，也就是#141 #142检测链表有无自环的快慢指针法来检测有没有循环。这个做法使得空间复杂度降到O(1)。

```C
int digitSquareSum(int n) {
    int sum = 0, tmp;
    while (n) {
        tmp = n % 10;
        sum += tmp * tmp;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    int slow, fast;
    slow = fast = n;
    do {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(fast);
        if (fast == 1) return 1; //reduce numbers of loops
        fast = digitSquareSum(fast);
        if(fast == 1) return 1;
    } while(slow != fast);
    return 0;
}
```
