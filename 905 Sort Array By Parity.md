# 905. Sort Array By Parity

## 题目

把一个数组奇偶分开。

>Given an array A of non-negative integers, return an array consisting of all the even elements of A, followed by all the odd elements of A.
>
>You may return any answer array that satisfies this condition.
>
>Example 1:
>
>>Input: [3,1,2,4]  
>>Output: [2,4,3,1]  
>>The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
>
>**Note:**
>
> - `1 <= A.length <= 5000`
> - `0 <= A[i] <= 5000`

## 解法

### 2-pass

分奇偶遍历两次。时间复杂度和空间复杂度都是O(N)。

```java
public int[] sortArrayByParity(int[] A) {
        int[] ans = new int[A.length];
        int i = 0;
        for (int a : A)
            if (a  % 2 == 0)
                ans[i++] = a;
        for (int a : A)
            if (a % 2 == 1)
                ans[i++] = a;
        return ans;
    }
```

### 1-pass

用两个指针从头和尾部开始，逐个判断，使得i指针向左的数都为偶数，j右边的数都为奇数。按照A[i]和A[j]的奇偶关系可分四种情况：

偶数，奇数： 最好的情况，不用动。i++, j--;  
偶数，偶数： i++;  
奇数，偶数： 两个元素交换位置。i++, j--;  
奇数，奇数： j--;  

直到两个指针相遇。时间复杂度O(N)，由于是in-place的排序，所以空间复杂度O(1)。上面四种情况又可以用代码中的三个if涵盖在内。

```java
    public int[] sortArrayByParity(int[] A) {
        for (int i = 0, j = A.length - 1; i< j; ){
            if (A[i] % 2 == 1 && A[j] % 2 == 0) {
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
            if (A[i] % 2 == 0 ) i++;
            if (A[j] % 2 == 1 ) j--;
        }
        return A;
    }
```
