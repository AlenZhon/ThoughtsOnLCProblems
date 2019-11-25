# 989. Add to Array-Form of Integer

## 题目

给定一个数组A，和一个整数K。A的每一个元素存着一个0-9的数字，所以整个数组可以表示一个非常大的数。现在求这个非常大的数与K相加之后的值，也用数组的形式返回。

>For a non-negative integer X, the array-form of X is an array of its digits in left to right order.  For example, if X = 1231, then the array form is [1,2,3,1].
>
>Given the array-form A of a non-negative integer X, return the array-form of the integer X+K.
>
>**Example 1:**
>
>>Input: A = [1,2,0,0], K = 34  
>>Output: [1,2,3,4]  
>>Explanation: 1200 + 34 = 1234
>
>**Example 2:**
>
>>Input: A = [2,7,4], K = 181  
>>Output: [4,5,5]  
>>Explanation: 274 + 181 = 455
>
>**Example 3:**
>
>>Input: A = [2,1,5], K = 806  
>>Output: [1,0,2,1]  
>>Explanation: 215 + 806 = 1021  
>
>**Example 4:**
>
>>Input: A = [9,9,9,9,9,9,9,9,9,9], K = 1  
>>Output: [1,0,0,0,0,0,0,0,0,0,0]  
>>Explanation: 9999999999 + 1 = 10000000000
>
>**Note：**  
>
> - 1 <= A.length <= 10000
> - 0 <= A[i] <= 9
> - 0 <= K <= 10000
> - If A.length > 1, then A[0] != 0

## 解法

高精度加法。从最后一位开始加起。由于K远小于Integer.MAX_VALUE，所以可取消进位变量，直接用K+A[i]，再将`(K + A[i]) % 10`存入数组，更新K值为`(K+A[i])/10`

时间复杂度和空间复杂度都是O(max(m, n))，两者分别是数组A的长度和K的位数。

```java
public List<Integer> addToArrayForm(int[] A, int K) {
        List<Integer> ret = new ArrayList<>();
        int i = A.length -1, x = K;
        while (i >=0 || x > 0) {
            if (i >= 0) x += A[i];
            ret.add(x % 10);
            x /= 10;
            i--;
        }
        Collections.reverse(ret);
        return ret;
    }
```

如果不想最后才对列表翻转，可将ret定义为 `LinkedList<Integer>()`，即可使用`.addFirst()`将元素插入到表头。

```java
public List<Integer> addToArrayForm(int[] A, int K) {
        LinkedList<Integer> ret = new LinkedList<>();
        int i = A.length -1, x = K;
        while (i >=0 || x > 0) {
            if (i >= 0) x += A[i];
            ret.addFirst(x % 10);
            x /= 10;
            i--;
        }
        return ret;
    }
```
