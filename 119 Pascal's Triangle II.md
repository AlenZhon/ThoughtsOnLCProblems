# 119 Pascal's Triangle II

## 题目描述

生成Pascal三角形的第k行，其中k不大于33，且k从0开始。

## 怎么解的

k不大于33，保证了其中最大的数值不超过`Integer.MAX_VALUE`。

在#118 改一改存储结构即可。时间复杂度O(k^2)，空间复杂度近似O(k^2)。

```java
 public List<Integer> getRow(int rowIndex) {
        List<Integer> ans = new ArrayList<Integer>(rowIndex + 1);
        if (rowIndex == 0) {
            ans.add(1);
            return ans;
        }
        for (int i = 1; i< rowIndex +1; i++) {
            List<Integer> newrow = new ArrayList<>();
            newrow.add(1);

            for (int j = 1; j < i; j ++) {
                newrow.add(ans.get(j-1) + ans.get(j));
            }
            newrow.add(1);
            ans = newrow;
        }
        return ans;
    }
```

Follow up 中要求提出一种只使用O(k)个额外空间的解法。即一开始申请好空间，每次迭代时从后往前更新数值。用了`Integer[k+1]`数组存储，最后返回时使用Arrays.asList转换类型。

```java
public List<Integer> getRow(int rowIndex) {
        Integer[] ans = new Integer[rowIndex + 1];  
        Arrays.fill(ans, 0);
        ans[0] = 1;
        for (int i = 1; i< rowIndex +1; i++) {
            for (int j = i; j > 0; j--) {
                ans[j] += ans[j - 1];
            }
        }
        return Arrays.asList(ans);
    }
```
