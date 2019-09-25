# 455. Assign Cookies

## 题目

有一群孩子想要你手上的不同大小的饼干。每个孩子对想要饼干的大小有一个预期，如果你给的饼干达到了预期他/她就会很开心。现在给定所有孩子的预期和饼干的大小，计算最多能让几个孩子很开心。注意，**每个孩子只能分到至多一块饼干**。

可以假设饼干预期始终为正（还有孩子不想要饼干也很开心的吗2333）。
>Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie. Each child i has a greed factor gi, which is the minimum size of a cookie that the child will be content with; and each cookie j has a size sj. If sj >= gi, we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.
>
>**Note:**
>
> - You may assume the greed factor is always positive.
> - You cannot assign more than one cookie to one child.
>
>**Example 1:**
>
>>Input: [1,2,3], [1,1]  
>>Output: 1  
>>Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3.  
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
>
>**Example 2:**
>
>>Input: [1,2], [1,2,3]  
>>Output: 2  
>>Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2.  
You have 3 cookies and their sizes are big enough to gratify all of the children,
You need to output 2.

## 解法

straight-forward. 对两个数组排序，即先满足预期比较小的朋友。用`i, j`指针遍历，如果s[j]>=g[i]那么轮到下一个小朋友。最后看有几个小朋友拿到了饼干即可（因为没拿到饼干的肯定不满意）。

```java
public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0, j = 0;
        while (i < g.length && j < s.length) {
            if (s[j++] >= g[i])
                i++;
        }
        return i;
    }
```
