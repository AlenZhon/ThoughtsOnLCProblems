# 697. Degree of an Array

## 题目

定义一个数组的度为数组里出现最频繁的元素的出现次数。给定一个数组，求一个满足如下条件的子数组长度，使得该子数组和原数组的度相同。

>Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.
>
>Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.
>
>Example 1:
>
>>Input: `[1, 2, 2, 3, 1]`  
>>Output: 2  
>>Explanation:  
>>The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
`[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]`
The shortest length is 2. So return 2.
>
>Example 2:
>
>>Input: [1,2,2,3,1,4,2]
>>Output: 6
>
>**Note:**
>
> - nums.length will be between 1 and 50,000.
> - nums[i] will be an integer between 0 and 49,999.

## 解法

用了一个`int[50000] count`用来存元素出现的次数，一个`int[50000][2] index`分别存元素出现的左下标和右下标。那么问题转化为在`count`中找到出现次数最多的元素（可能有多个），且该元素i对应的`index[1] - index[0] + 1`最小。

```java
public int findShortestSubArray(int[] nums) {
        int[] count = new int[50000];
        int[][] index = new int[50000][2];
        for (int i =0; i< nums.length; i++){
            if (index[nums[i]][0] != 0 || nums[i] == nums[0])
                index[nums[i]][1] = i;
            else
                index[nums[i]][0] = i;
            count[nums[i]]++;
        }
        int degree = 1, maxNum = -1, minLen = 1;
        for (int j =0; j< count.length; j++){
            if (count[j] > degree) {
                degree = count[j];
                minLen = index[j][1] - index[j][0] + 1;
            } else if (count[j] == degree && degree > 1)
                minLen = Math.min(minLen, index[j][1] - index[j][0] + 1);
        }
        return minLen;
    }
```

然而AC后发现运行时间106ms，存储空间也只打败了5%的提交。估计是count和index数组太稀疏。改用一下HashMap。

```java
public int findShortestSubArray(int[] nums) {
        HashMap<Integer, Integer> count = new HashMap(),
        left = new HashMap(), right = new HashMap();
        for (int i =0; i< nums.length; i++){
            int n = nums[i];
            if (left.get(n) == null)
                left.put(n, i);
            else
                right.put(n, i);
            count.put(n, count.getOrDefault(n, 0) + 1);
        }
        int degree = 1, minLen = 1;
        for (int key : count.keySet()){
            if (count.get(key) > degree) {
                degree = count.get(key);
                minLen = right.get(key) - left.get(key) + 1;
            } else if (degree > 1 && count.get(key) == degree)
                minLen = Math.min(minLen, right.get(key) - left.get(key) + 1);
        }
        return minLen;
    }
```

时间复杂度O(N)，空间复杂度O(N)。运行时间降到了25ms。Solution中也是用的这个解法，不过在计算度的时候使用了`int degree = Collections.max(count.values());` 然后直接判断

```java
if (count.get(key) == degree) {
    ans = Math.min(ans, right.get(key) - left.get(key) + 1);
}
```

把三个HashMap合成一个`HashMap<Integer, int[]>`，其中`int[]`存储**`[出现次数、第一次出现的索引，最后一次出现的索引]`**三元组。

```java
public int findShortestSubArray(int[] nums) {
        HashMap<Integer, int[]> count = new HashMap();
        for (int i = 0; i< nums.length; i++){
            if (!count.containsKey(nums[i])){
               count.put(nums[i], new int[]{1, i, 0});  // the first element in array is degree, second is first index of this key, third is last index of this key
           } else {
               int[] temp = count.get(nums[i]);
               temp[0]++;
               temp[2] = i;
           }
        }
        int degree = 1, minLen = 1;
        for (int[] value : count.values())
            if (value[0] > degree) {
                degree = value[0];
                minLen = value[2] - value[1] + 1;
            } else if (value[0] == degree && degree > 1)
                minLen = Math.min(minLen, value[2] - value[1] + 1);
        return minLen;
    }
```

2ms的解法是先遍历数组找到数组中最大元素`max`，再根据max的大小构造`count, left, right`数组。(如果数组里只有一个49999，其他都是小于100的数，那不就亏了)。

```java
public int findShortestSubArray(int[] nums) {
    if(nums.length<2) return nums.length;
    int res = nums.length;
    int max = Integer.MIN_VALUE;
    for (int x : nums) {
        max = Math.max(x, max);
    }
    int maxFreq = 1;
    int[] b = new int[max + 1];
    int[] l = new int[max + 1];
    int[] r = new int[max + 1];
    for (int i = 0; i < nums.length; i++) {
        b[nums[i]]++;
        if (b[nums[i]] == 1) {
            l[nums[i]] = i;
        }
        r[nums[i]] = i;
        maxFreq = Math.max(maxFreq, b[nums[i]]);
    }
    for (int i = 0; i < b.length; i++) {
        if (b[i] == maxFreq)
          res = Math.min(res, r[i] - l[i] + 1);
    return res;
}
```
