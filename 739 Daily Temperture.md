# 739. 每日温度

## 题目

根据每日 气温 列表，请重新生成一个列表，对应位置的输出是需要再等待多久温度才会升高超过该日的天数。如果之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`，你的输出应该是 `[1, 1, 4, 2, 1, 1, 0, 0]`。

**提示：** 气温 列表长度的范围是 `[1, 30000]`。每个气温的值的均为华氏度，都是在 `[30, 100]` 范围内的整数。

## 解法

### Approach 1
暴力求解就从左到右遍历 两层循环。时间复杂度O(n^2)空间复杂度O(1)。
考虑了一下如果存一个最大值的下标是否会运行时间是否会少一些，但收效不大。

### Approach 2
由于温度都是有范围的整数，可以用哈希数组存最高温度的索引值。
从后向前遍历，假设当前遍历到T[i]，则在哈希数组的`(T[i], 100]`中寻找最小的索引值。
最后更新T[i]在数组中的索引值。
时间复杂度O(NW)，由于题目规定温度在[30,100]， 所以W= 71，空间复杂度O(N + W)。

```java
 public int[] dailyTemperatures(int[] T) {
        int[] ret = new int[T.length];
        int[] hash = new int[101];
        Arrays.fill(hash, Integer.MAX_VALUE);
        for (int i = T.length - 1; i>=0; i--){
            int maxIndex = Integer.MAX_VALUE;
            for (int j = T[i] + 1; j <=100; j++){
                if (hash[j] < maxIndex)
                    maxIndex = hash[j];
            }
            if (maxIndex < Integer.MAX_VALUE){
                ret[i] = maxIndex - i; 
            }
            hash[T[i]] = i;
        }
        return ret;
    }
```
### Approach 3

在考虑暴力求解的时候发现问题： 考虑[75, 71, 72, 69, 76]，一开始maxIndex赋值到76对应的索引，但i增加时，71并不需要遍历到76只需要72就行。如果从后向前遍历，那么maxIndex应该需要存不止一个值，对于72和69来说是76对应的4，对于71来说是72对应的2， 对于75来说又是76对应的4。

一个单调栈的典型应用。从后向前遍历，维护一个单调栈存储最高温度的索引，要求栈顶到栈底索引对应的温度是递增的。

```java
public int[] dailyTemperatures(int[] T) {
        int[] ret = new int[T.length];
        Stack<Integer> s = new Stack<>();
        for (int i = T.length -1; i>=0; i--){
            while (!s.isEmpty() && T[i] >= T[s.peek()]) s.pop();
            ret[i] = s.isEmpty() ? 0 : s.peek() - i;
            s.push(i);
        }
        return ret;
    }
```


