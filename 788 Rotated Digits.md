# 788. Rotated Digits

## 题目

`[0-9]`十个数字之中， 0, 1, 8旋转180度还是自己，2, 5和6, 9旋转180度变成对方。3, 4, 7旋转180度之后变成无效数字。现在给出一个正整数 N (`1<=N <=10000`)，求`[1, N]`中有多少个数字每位旋转180度之后仍是有效数字。

>X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X.  Each digit must be rotated - we cannot choose to leave it alone.
>
>A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number and become invalid.
>
>Now given a positive number N, how many numbers X from 1 to N are good?
>
>Example:
>>Input: 10  
>>Output: 4  
>>Explanation:  
>>There are four good numbers in the range `[1, 10]` : 2, 5, 6, 9.
>>Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.
>
>**Note:**
>
> - N  will be in range `[1, 10000]`.

## 解法

粗暴解法。遍历1-N，判断每个数位。如果有3,4,7直接跳过，其他的数字里有2,5,6,9说明不同。

```java
public int rotatedDigits(int N) {
        int count = 0;
        for (int i = 1; i<= N; i++) {
            int x = i;
            boolean flag = false;
            while(x > 0){
                int n = x % 10;
                x /=10;
                if (n == 2 || n == 5 || n == 6 || n == 9)
                    flag = true;
                else if (n == 3 || n == 4 || n == 7) {
                    flag = false;
                    break;
                }
            }
            if (flag) count++;
        }
        return count;
    }
```

实际上，这道题可以转化为“给定一个数值上限，用[0,1,2,5,6,8,9]构成的数 - 用[0, 1, 8]构成的数”。

```java
final private int[] cand1 = new int[]{0, 1, 2, 5, 6, 8, 9};
    final private int[] cand2 = new int[]{0, 1, 8};

    public int rotatedDigits(int N) {
        return helper(cand1, N) - helper(cand2, N);
    }

    public int helper(int[] cand, int N) {
        List<Integer> digits = new ArrayList<>();
        while (N > 0) {
            digits.add(N % 10);
            N /= 10;
        }

        int ans = 0;
        boolean cont = true;
        for (int i = digits.size() - 1; i >= 0; i--) {
            if (cont == false) break;
            cont = false;
            for (int j = 0; j < cand.length; j++) {
                if (digits.get(i) > cand[j]) {
                    ans += Math.pow(cand.length, i);
                } else if (digits.get(i) == cand[j]) {
                    cont = true;
                    if (i == 0) ans += 1;
                } else {
                    break;
                }
            }
        }

        return ans;
    }
```
