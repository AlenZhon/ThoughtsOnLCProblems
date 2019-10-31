# 717. 1-bit and 2-bit Characters

## 题目

我们有两个特殊的字符。第一个字符可以用`0`表示，第二个字符可以用两个比特（`10`或`11`）表示。给定一个01数组，其末尾元素固定为0。判断这个数组的末尾元素是否可以用来表示第一个字符。

例如`[1,1,1,0]`，只能解码成`11`,`10`。所以末尾元素不表示第一个字符，返回`false`。

>We have two special characters. The first character can be represented by one bit 0. The second character can be represented by two bits (10 or 11).
>
>Now given a string represented by several bits. Return whether the last character must be a one-bit character or not. The given string will always end with a zero.
>
>**Example 1:**
>
>>Input:  
>>bits = [1, 0, 0]  
>>Output: True  
>>Explanation:  
>>The only way to decode it is two-bit character and one-bit character. So the last character is one-bit character.
>
>**Example 2:**
>
>>Input:  
>>bits = [1, 1, 1, 0]  
>>Output: False  
>>Explanation:  
>>The only way to decode it is two-bit character and two-bit character. So the last character is NOT one-bit character.
>
>Note:
>
> - `1 <= len(bits) <= 1000`.
> - `bits[i]` is always 0 or 1.

## 解法

读题目读了好久...  
没想到什么骚解法，所以还是一个个遍历，判断i应该加1还是2，最后判断i的位置返回真假。时间复杂度O(n)，空间复杂度O(1)。

```java
public boolean isOneBitCharacter(int[] bits) {
        if (bits.length == 2 && bits[0] == 1) return false;
        int i = 0;
        while (i <= bits.length - 2) {
            if (bits[i] == 0)
                i++;
            else if ((bits[i] ==1 && bits[i+1] == 1) || (bits[i] == 1 && bits[i + 1] == 0))
                i+=2;
        }
        return i == bits.length -1;
    }
```

其中由于`10`和`11`时都加2，`0`时加1。可以认为指针每次自增的值是 `bits[i] + 1`。所以可以简写为：

```java
public boolean isOneBitCharacter(int[] bits) {
        if (bits.length == 2 && bits[0] == 1) return false;
        int i = 0;
        while (i <= bits.length - 2) {
            i+= bits[i] + 1;
        }
        return i == bits.length -1;
    }
```
