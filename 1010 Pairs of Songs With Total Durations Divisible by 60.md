# 1010. Pairs of Songs With Total Durations Divisible by 60

## 题目

给定一个列表`time[]`，里面每个元素`time[i]`表示一首歌的时间（以秒为单位），如果两首歌的时间之和能被60秒整除则称这两首歌为一对，请问这个列表中有多少对？

>In a list of songs, the i-th song has a duration of `time[i]` seconds.
>
>Return the number of pairs of songs for which their total duration in seconds is divisible by 60.  Formally, we want the number of indices `i < j` with `(time[i] + time[j]) % 60 == 0`.
>
>**Example 1:**
>
>>Input: [30,20,150,100,40]  
>>Output: 3  
>>Explanation: Three pairs have a total duration divisible by 60:
>>(time[0] = 30, time[2] = 150): total duration 180
>>(time[1] = 20, time[3] = 100): total duration 120
>>(time[1] = 20, time[4] = 40): total duration 60
>
>**Example 2:**
>
>>Input: [60,60,60]  
>>Output: 3  
>>Explanation: All three pairs have a total duration of 120, which is divisible by 60.
>
>**Note:**
>
> - `1 <= time.length <= 60000`
> - `1 <= time[i] <= 500`

## 解法

用一个`int[]count = new int[60]`存储 `(time[i] % 60)` 相同的歌的数量，比如60秒的歌，就把count[0]自增1。这样就可以直接计算了。

注意count[0]和count[30]需要特意处理一下。

```java
public int numPairsDivisibleBy60(int[] time) {
        int[] count = new int[60];
        for (int t : time)
            count[t % 60]++;
        int ret = 0;
        for (int i = 0; i<= 30; i++){
            if (i == 0 || i == 30){
                if (count[i] > 0)
                    ret += count[i] * (count[i] - 1) / 2;
            } else
                if (count[i] > 0 && count[60 - i] > 0)
                    ret += count[i] * count[60 - i];
        }
        return ret;
    }
```

时间复杂度O(N)，空间复杂度O(1)。
