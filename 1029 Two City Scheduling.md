# 1029. Two City Scheduling

## 题目

现在有2N个人要选择去城市A或者城市B面试。给定这些人到两个城市所需要花费的钱，要求找到一种调度方案，使得到城市A和城市B面试的人数都为N，且花费的钱最少。

>There are 2N people a company is planning to interview. The cost of flying the i-th person to city A is `costs[i][0]`, and the cost of flying the i-th person to city B is `costs[i][1]`.
>
>Return the minimum cost to fly every person to a city such that exactly N people arrive in each city.
>
>Example 1:
>
>>Input: [[10,20],[30,200],[400,50],[30,20]]  
>>Output: 110  
>>Explanation:  
>>The first person goes to city A for a cost of 10.  
>>The second person goes to city A for a cost of 30.  
>>The third person goes to city B for a cost of 50.  
>>The fourth person goes to city B for a cost of 20.  
>>
>>The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.
>
>**Note:**
>
> - 1 <= costs.length <= 100
> - It is guaranteed that costs.length is even.
> - 1 <= costs[i][0], costs[i][1] <= 1000

## 解法

### sorting

可以比较每个人去A城和去B城的花费差值，把差值小的前N个人安排到A城。时间复杂度为排序的O(nlogn)，空间复杂度相当于O(1)（用的Arrays.sort()方法是in-place的）。

使用`Arrays.sort()`的方法按照差值大小排列数据。

```java
public int twoCitySchedCost(int[][] costs) {
        int n = costs.length / 2;
        Arrays.sort(costs, (a, b) -> ((a[0] - a[1]) - (b[0] - b[1])));
        int sum = 0;
        for (int[] cost : costs) {
            if (--n >= 0) sum+= cost[0];
            else sum+= cost[1];
        }
        return sum;
    }
```

其中sort方法相当于重写了compare方法。

```java
Arrays.sort(costs, new Comparator<int[]>() {
        public int compare(int[] a, int[] b) {
            return (a[0] - a[1]) - (b[0] - b[1]);
        }
    });
```

## Dynamic Programing

来自[讨论区](https://leetcode.com/problems/two-city-scheduling/discuss/278731/Java-DP-Easy-to-Understand)

>`dp[i][j]` represents the cost when considering first `(i + j)` people in which `i` people assigned to city A and `j` people assigned to city B.

```java
public int twoCitySchedCost(int[][] costs) {
        int N = costs.length / 2;
        int[][] dp = new int[N + 1][N + 1];
        for (int i = 1; i <= N; i++) {
            dp[i][0] = dp[i - 1][0] + costs[i - 1][0];
        }
        for (int j = 1; j <= N; j++) {
            dp[0][j] = dp[0][j - 1] + costs[j - 1][1];
        }
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                dp[i][j] = Math.min(dp[i - 1][j] + costs[i + j - 1][0], dp[i][j - 1] + costs[i + j - 1][1]);
            }
        }
        return dp[N][N];
    }
```

用一个二维数组，每个元素存储迭代后的成本。先初始化第0行和第0列，相当于把所有人都安排去A城和把所有人都安排去B城。每一步迭代，对于第(i+j)个人，需要判断把TA安排在哪一座城，也就是在`(dp[i - 1][j] + costs[i + j - 1][0], dp[i][j - 1] + costs[i + j - 1][1])`之中选取最小值作为当前成本。时间复杂度和空间复杂度都是O(n^2)。
