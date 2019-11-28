# 860. Lemonade Change

## 题目

你是一个卖柠檬水的柜员。一杯柠檬水5刀，顾客排着队来买，已知他们拿的是以下三种纸币的任意一种：5刀，10刀，20刀。你手里一点找零的纸币都没有，所以完全用顾客的钱来找。现在给定顾客们手里拿的钱，判断你能不能顺利地给每个人找零。

>At a lemonade stand, each lemonade costs $5.
>
>Customers are standing in a queue to buy from you, and order one at a time (in the order specified by bills).
>
>Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill.  You must provide the correct change to each customer, so that the net transaction is that the customer pays $5.
>
>Note that you don't have any change in hand at first.
>
>Return true if and only if you can provide every customer with correct change.
>
>**Example 1:**
>
>>Input: [5,5,5,10,20]  
>>Output: true  
>>Explanation:  
>>From the first 3 customers, we collect three $5 bills in order.  
>>From the fourth customer, we collect a $10 bill and give back a $5.  
>>From the fifth customer, we give a $10 bill and a $5 bill.  
>>Since all customers got correct change, we output true.  
>
>**Example 2:**
>
>>Input: [5,5,10]  
>>Output: true
>
>**Example 3:**
>
>>Input: [10,10]  
>>Output: false
>
>**Example 4:**
>
>>Input: [5,5,10,10,20]  
>>Output: false  
>>Explanation:  
>>From the first two customers in order, we collect two $5 bills.  
>>For the next two customers in order, we collect a $10 bill and give back a $5 bill.  
>>For the last customer, we can't give change of $15 back because we only have two $10 bills.  
>>Since not every customer received correct change, the answer is false.
>
>**Note:**
>
> - `0 <= bills.length <= 10000`
> - `bills[i]` will be either 5, 10, or 20.

## 解法

计两个变量表示手头上有的5刀和10刀数量。如果顾客给10刀，就找个5刀，没有5刀就返回false。如果顾客给20刀，先判断有没有10+5，再判断有没有三个5刀，都没有的话就返回false。

时间复杂度O(N)，空间O(1)

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0, ten = 0;
        for (int bill : bills)
            switch (bill) {
                case 5:
                    five++;
                    break;
                case 10:
                    ten++;
                    if (five == 0) return false;
                    five--;
                    break;
                case 20:
                    if (ten > 0 && five > 0) {
                        ten--;
                        five--;
                    } else if (ten == 0 && five > 2) {
                        five-= 3;
                    } else
                        return false;
                    break;
            }
        return true;
    }
}
```