# 690. Employee Importance

## 题目

以列表的形式给出表示雇员信息的三元组`<int id, int importance, List<Integer> subordinates>`，分别表示雇员id，雇员的价值以及雇员的**直系**下属。现在给出某个雇员的id，返回TA及其下属的价值之和。

>You are given a data structure of employee information, which includes the employee's unique id, his importance value and his **direct** subordinates' id.
>
>For example, employee 1 is the leader of employee 2, and employee 2 is the leader of employee 3. They have importance value 15, 10 and 5, respectively. Then employee 1 has a data structure like `[1, 15, [2]]`, and employee 2 has `[2, 10, [3]]`, and employee 3 has `[3, 5, []]`. Note that although employee 3 is also a subordinate of employee 1, the relationship is **not direct**.
>
>Now given the employee information of a company, and an employee id, you need to return the total importance value of this employee and all his subordinates.
>
>**Example 1:**
>
>>**Input:** `[[1, 5, [2, 3]], [2, 3, []], [3, 3, []]]`, 1
>>**Output:** 11  
>>**Explanation:**  
Employee 1 has importance value 5, and he has two direct subordinates: employee 2 and employee 3. They both have importance value 3. So the total importance value of employee 1 is `5 + 3 + 3 = 11`.
>
>**Note:**
>
>- One employee has at most one **direct** leader and may have several subordinates.
>- The maximum number of employees won't exceed 2000.

## 解法

一开始没有认真审题。以为只是求该雇员和其直系下属的价值之和。

用了一个`HashMap<Integer, Employee>`预存所有雇员的id和对应信息，降低查找所用的时间。累加价值的时候可以使用递归/非递归写法。假设n为雇员个数，则时间复杂度O(n)，空间复杂度O(n)。

### 非递归

```java
public int getImportance(List<Employee> employees, int id) {
        HashMap<Integer, Employee> map = new HashMap<>();
        for (Employee e : employees)
            map.put(e.id, e);
        Queue<Integer> q = new LinkedList<>();
        int value = 0;
        q.offer(id);
        while (!q.isEmpty()) {
            Integer currId = q.poll();
            value+= map.get(currId).importance;
            for (Integer sub : map.get(currId).subordinates)
                q.offer(sub);
        }
        return value;
    }
```

### 递归

```java
public int getImportance(List<Employee> employees, int id) {
        HashMap<Integer, Employee> map = new HashMap<>();
        for (Employee e : employees)
            map.put(e.id, e);
        return getValue(map, id);
    }
    private int getValue(HashMap<Integer, Employee> map, int id) {
        int value = map.get(id).importance;
        for (Integer sub : map.get(id).subordinates)
            value+= getValue(map, sub);
        return value;
    }
```
