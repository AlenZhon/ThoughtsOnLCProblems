# 176. Second Highest Salary

## 题目要求

给定一张Employee表，字段是（id,Salary) 要求查出第二高的Salary。

>Write a SQL query to get the second highest salary from the Employee table.
>
>  
>| Id | Salary |  
>|:---:|:---:|
>| 1  | 100    |  
>| 2  | 200    |  
>| 3  | 300    |
>
>For example, given the above Employee table, the query should return `200` as the second highest salary. If there is no second highest salary, then the query should return `null`.
>
>| SecondHighestSalary |  
>|:---:|
>| 200                 |

## 怎么写的

>Approach: Using sub-query and `LIMIT` clause [Accepted]
>
>**Algorithm**
>
>Sort the distinct salary in descend order and then utilize the `LIMIT` clause to get the second highest salary.
>
>```SQL
>select (
>select distinct Salary as SecondHighestSalary from Employee
>order by Salary desc limit 1 offset 1) as SecondHighestSalary
>```

其中`distinct`关键字使得第一次查询时Salary值不重复。`limit`设定返回的记录数，`offset`设定指定select语句开始查询的数据偏移量。
