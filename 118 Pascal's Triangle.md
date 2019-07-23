# 118 Pascal's Triangle

## 题目描述

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

Pascal三角，也叫做杨辉三角形，本质是（a+b）的n次幂展开式中各个子式的常系数。

## 解法

设置好边界值，迭代生成三角形的每一行。  
当行数i（i>2），列数j时：  

a[i][j] = a[i-1][j-1] + a[i-1][j].

```java
public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        if (numRows == 0) {return ans;}

        ans.add(new ArrayList<>());
        ans.get(0).add(1);

        for (int i= 1; i< numRows; i++) {
            List<Integer> newrow = new ArrayList<>();
            newrow.add(1);

            for (int j = 1; j < i; j ++) {
                newrow.add(ans.get(i-1).get(j-1) + ans.get(i-1).get(j));
            }
            newrow.add(1);
            ans.add(newrow);
        }
        return ans;
    }
```

## Notes

由于题目里要求返回`List<List<Integer>>`， 故每次迭代实例化一个ArrayList用于存储每行的数据。不能new List<>，会报错`List is abstract; cannot be instantiated`。

用 `add()`和 `get()`方法在ArrayList中添加和获取数据。

跳过了一些binary tree的题目没做是想找个时间复习一下数据结构，然而最近在构思论文思路，所以略忙。
