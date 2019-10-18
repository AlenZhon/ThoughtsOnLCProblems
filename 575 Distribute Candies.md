# 575. Distribute Candies

## 题目

一堆糖果共有`2n`块，用一个数组表示。数组元素的值表示这块糖果属于第几类。将这堆糖果平均分给一男一女两个人。求女生手中的n块糖果最多可以有几类。

>Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.
>
>**Example 1:**
>>
>>Input: candies = `[1,1,2,2,3,3]`  
>>Output: 3  
>>Explanation:  
>>There are three different kinds of candies (1, 2 and 3), and two candies for each kind.  
Optimal distribution: The sister has candies `[1,2,3]` and the brother has candies `[1,2,3]`, too.  
The sister has three different kinds of candies.  
>
>**Example 2:**
>
>>Input: candies = [1,1,2,3]  
>>Output: 2  
>>Explanation: For example, the sister has candies [2,3] and the brother has candies [1,1].  
>>The sister has two different kinds of candies, the brother has only one kind of candies.  
>
>**Note:**
>
> - The length of the given array is in range `[2, 10,000]`, and will be even.
> - The number in given array is in range `[-100,000, 100,000]`.

## 解法

由于女生手中只有n块糖果，那么糖果种类的上限就是n。用一个Set代表女生拿的糖果种类，遍历数组添加到Set里。Set的容量上限是n。

```java
public int distributeCandies(int[] candies) {
        Set<Integer> set = new HashSet<>();
        for (int candy : candies) {
            set.add(candy);
            if (set.size() > candies.length / 2) return candies.length /2;
        }
        return set.size();
    }
```

如果用一个哈希数组实现则是这样的。

```java
public int distributeCandies(int[] candies) {
        int[] hash = new int[200001];
        int kind = 0;
        for (int i = 0; i < candies.length && kind < candies.length / 2; i++) {
            if (hash[ candies[i] + 100000 ]++ == 0) kind++;
        }
        return kind;
    }
```

时间复杂度O(n)，用Set的空间复杂度最坏情况下达到O(n)，而哈希数组的空间复杂度是确定常数（虽然比较大）。

此外，还可以先对数组进行排序。

```java
public int distributeCandies(int[] candies) {
        Arrays.sort(candies);
        int count = 1;
        for (int i = 1; i < candies.length && count < candies.length / 2; i++)
            if (candies[i] > candies[i - 1])
                count++;
        return count;
    }
```

时间复杂度主要是排序的O(nlogn)，空间O(1)
