# 177. Nth Highest Salary

## 题目要求

给定一张Employee表，字段是（id,Salary) 要求查出第n高的Salary。

>Write a SQL query to get the nth highest salary from the Employee table.
>
>| Id | Salary |  
>|:---:|:---:|
>| 1  | 100    |  
>| 2  | 200    |  
>| 3  | 300    |  
>
>For example, given the above Employee table, the nth highest salary where n = 2 is `200`. If there is no nth highest salary, then the query should return `null`.
>
>| getNthHighestSalary(2) |  
>|:---:|
>| 200                    |
>

## 怎么写的

和176差不多咯。把offset改成n-1。  
然而SQL里limit和offset似乎只接受numeric constants。所以先声明变量 `declare M INT default N-1;`

```SQL
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  DECLARE M INT DEFAULT N-1;
  RETURN (
      # Write your MySQL query statement below.
      select (
        select distinct Salary as SecondHighestSalary from Employee
        order by Salary desc limit 1 offset M) as SecondHighestSalary
  );
END
```
