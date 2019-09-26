# 461. Hamming Distance

## 题目

两个正整数，计算他们的汉明距离。

>The Hamming distance between two integers is the number of positions at which the corresponding bits are different.
>
>Given two integers x and y, calculate the Hamming distance.
>
>**Note:**  
>`0 ≤ x, y < 2^31`
>
>**Example:**  
>>Input:  
>>x = 1, y = 4  
>>Output:  
>>2  
>>Explanation:  
>>1   (0 0 0 1)  
>>4   (0 1 0 0)  
>>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↑&nbsp;&nbsp;&nbsp;&nbsp;↑
>>
>>The above arrows point to positions where the corresponding bits are different.

## 解法

对于通信狗来说汉明距离还是比较熟悉的了。记录下两数异或后1的个数。

如果用`Integer.bitCount(int x)`的话一行就可以搞定。

`return Integer.bitCount(x ^ y);`

或者

```java
public int hammingDistance(int x, int y) {
        int hamming = x ^ y, count = 0;
        for (int i = 0; i< 32; i++)
            count += ((hamming>>i) & 1);
        return count;
    }
```
