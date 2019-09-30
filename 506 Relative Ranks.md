# 506. Relative Ranks

## 题目

N个运动员的比赛分数各不相同，找出他们的排名并返回金银铜牌。

>Given scores of N athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".
>
>**Example 1:**
>
>>Input: [5, 4, 3, 2, 1]  
>>Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]  
>>Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal".  
For the left two athletes, you just need to output their relative ranks according to their scores.
>
>**Note:**
>
> - N is a positive integer and won't exceed 10,000.
> - All the scores of athletes are guaranteed to be unique.

## 解法

主要就是把运动员的名次和对应的索引联系起来。

有没有一种办法可以用Arrays.sort()排序之后同时返回索引的啊？

由于所有得分互不相同，所以拿个HashMap记录了一下初始的分数下标，这样排序后一个一个查找下标约为O(1)。所以总体的时间复杂度是`Arrays.sort()`的`O(nlogn)`， 空间复杂度为`O(n)`。

```java
public String[] findRelativeRanks(int[] nums) {
        String[] res = new String[nums.length];
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        for (int i = 0; i< nums.length; i++)
            index.put(nums[i], i);

        Arrays.sort(nums); // ascending order
        for (int i = 0; i < nums.length; i++) {
            int rank = nums.length - i;
            if (rank == 1) res[index.get(nums[i])] = "Gold Medal";
            else if (rank == 2) res[index.get(nums[i])] = "Silver Medal";
            else if (rank == 3) res[index.get(nums[i])] = "Bronze Medal";
            else res[index.get(nums[i])] = ""+ rank;
        }
        return res;
    }
```

OJ里运行时间是7ms。时间更低的是自己用int[]做的一个hash数组。数组的容量是运动员所取得的最大分数（如果有一个运动员分数碾压别人，是不是造成较多的空间浪费哈哈哈哈哈）。

```java
public String[] findRelativeRanks(int[] nums) {
        String[] res = new String[nums.length];
        int max = 0;
        for (int n : nums) max = Math.max(max, n);
        int[] hash = new int[max + 1];

        for (int i = 0 ; i< nums.length; i++)
            hash[nums[i]] = i + 1; // zero as undifined
        int placing = 0;
        for (int i = hash.length -1; i>= 0; i--) {
            if (hash[i] == 0) continue;
            placing ++;
            switch (placing) {
                case 1:
                    res[hash[i] - 1] = "Gold Medal";
                    break;
                case 2:
                    res[hash[i] - 1] = "Silver Medal";
                    break;
                case 3:
                    res[hash[i] - 1] = "Bronze Medal";
                    break;
                default:
                    res[hash[i] - 1] = String.valueOf(placing);
                    break;
            }
        }
        return res;
    }
```
