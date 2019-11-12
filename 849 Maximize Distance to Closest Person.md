# 849. Maximize Distance to Closest Person

## 题目

有一排长座椅，1表示有人坐着，0表示空座位。ALEX 走进来的时候这排椅子上已经至少有一个人坐着了。但他比较自闭，想坐在一个离其他人都最远的座位上（即最大化他和最近的人的距离）。帮他找到此座位，返回最大距离。

>In a row of seats, 1 represents a person sitting in that seat, and 0 represents that the seat is empty.
>
>There is at least one empty seat, and at least one person sitting.
>
>Alex wants to sit in the seat such that the distance between him and the closest person to him is maximized.
>
>Return that maximum distance to closest person.
>
>**Example 1:**
>
>>Input: `[1,0,0,0,1,0,1]`  
>>Output: 2  
>>Explanation:  
>>If Alex sits in the second open seat (`seats[2]`), then the closest person has distance 2.  
>>If Alex sits in any other open seat, the closest person has distance 1.  
>>Thus, the maximum distance to the closest person is 2.  
>
>**Example 2:**
>
>>Input: `[1,0,0,0]`  
>>Output: 3  
>>Explanation:  
>>If Alex sits in the last seat, the closest person is 3 seats away.  
>>This is the maximum distance possible, so the answer is 3.  
>
>**Note:**
>
> - 1 <= `seats.length` <= 20000
> - seats contains only 0s or 1s, at least one 0, and at least one 1.

## 解法

和 *#605 Can place Flowers* 有点像。 two pointers 计算连续0的个数，然后分连续0在开头/在结尾，连续0在中间两种情况分别判断。

```java
public int maxDistToClosest(int[] seats) {
        int maxd = 0;
        for (int i = 0; i<seats.length; i++) {
            if (seats[i] == 0) {
                int j = i + 1;
                while (j < seats.length && seats[j] == 0) j++;
                int zeros = j - i;
                if (i == 0 || j == seats.length)
                    maxd = zeros > maxd ? zeros : maxd;
                else {
                    int half = zeros % 2 == 0 ? (zeros - 1) / 2 : (zeros - 1) / 2 + 1;
                    maxd = half > maxd ? half : maxd;
                }
                i = j;
            }
        }
        return maxd;
    }
```

时间复杂度O(N)，空间O(1).
