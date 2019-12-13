# 1237. Find Positive Integer Solution for a Given Equation

## 题目

现在有一个函数`f(x, y)`始终满足`f(x, y) < f(x + 1, y) && f(x, y) < f(x, y + 1)`，现在给定 z ，定义x,y 的定义域为`[1, 1000]`，找出所有满足`f(x, y) == z`的 (x, y)。

>Given a function  `f(x, y)` and a value z, return all positive integer pairs x and y where `f(x,y) == z`.
>
>The function is constantly increasing, i.e.:
>
> - f(x, y) < f(x + 1, y)
> - f(x, y) < f(x, y + 1)
>
>The function interface is defined like this:
>
>```java
>
>interface CustomFunction {
>public:
>  // Returns positive integer f(x, y) for any given positive integer x and y.
>  int f(int x, int y);
>};
>```
>
>For custom testing purposes you're given an integer `function_id` and a target z as input, where `function_id` represent one function from an secret internal list, on the examples you'll know only two functions from the list.  
>
>You may return the solutions in any order.
>
>**Example 1:**
>
>>Input: function_id = 1, z = 5  
>>Output: [[1,4],[2,3],[3,2],[4,1]]  
>>Explanation: function_id = 1 means that f(x, y) = x + y
>
>**Example 2:**
>
>>Input: function_id = 2, z = 5  
>>Output: [[1,5],[5,1]]  
>>Explanation: function_id = 2 means that f(x, y) = x * y  
>
>**Constraints:**
>
> - `1 <= function_id <= 9`
> - `1 <= z <= 100`
> - It's guaranteed that the solutions of `f(x, y) == z` will be on the range 1 <= x, y <= 1000
> - It's also guaranteed that f(x, y) will fit in 32 bit signed integer if 1 <= x, y <= 1000

## 解法

根据它的递增性，`f(1, 1000) < f(1000, 1000)`
初始化x = 1, y = 1000，始终保持f(x, y) <= z，搜索取等的情况。时间复杂度O(X + Y)

```java
public List<List<Integer>> findSolution(CustomFunction customfunction, int z) {
        List<List<Integer>> ret = new ArrayList();
        int x = 1, y = 1000;
        while (x < 1001 && y > 0){
            int tmp = customfunction.f(x, y);
            if (tmp < z) x++;
            else if (tmp > z) y--;
            else ret.add(Arrays.asList(x++, y--));
        }
        return ret;
    }
```

Solution里1ms的解法有一点投机取巧，把上限从1000设到了z。

```java
public List<List<Integer>> findSolution(CustomFunction customfunction, int z) {
        int low = 1, high = z;
        List<List<Integer>> ret = new LinkedList<>();
        while (low <= z && high > 0) {
            int curr = customfunction.f(low, high);
            if (curr == z)
                ret.add(Arrays.asList(low++, high--));
            else if (curr < z)
                low++;
            else if (curr > z)
                high--;
        }
        return ret;
    }
```
