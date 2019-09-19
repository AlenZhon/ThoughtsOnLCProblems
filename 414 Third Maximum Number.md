# 414. Third Maximum Number

## 题目

求一个数组中第三大的数。如果不存在，则返回最大值。要求时间复杂度控制在O(N)以内。

## 解法

定义三个`Integer`初始值为`null`，直接写。时间复杂度O(N)，空间复杂度O(1)。OJ 显示运行时间2ms。

```java
 public int thirdMax(int[] nums) {
        Integer max1 = null, max2= null, max3 =null;
        for (Integer n : nums) {
            if (n.equals(max1) || n.equals(max2) || n.equals(max3)) continue;
            if (max1 == null || n > max1) {
                max3 = max2;
                max2 = max1;
                max1 = n;
            } else if (max2 == null || n > max2) {
                max3 = max2;
                max2 =n;
            } else if (max3 == null || n > max3) {
                max3 = n;
            }
        }
        return max3 == null ? max1 : max3;
    }
```

但这样的写法没有普遍性。要是拓展到第k个最大的值上就不能定义k个变量了。这个问题参看 *#215. Kth Largest Element in an Array*
