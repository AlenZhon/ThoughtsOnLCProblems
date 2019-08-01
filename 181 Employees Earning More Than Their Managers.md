# 181. Employees Earning More Than Their Managers

## 题目描述

给定一张Employee数据表，字段为（PersonId, Name, Salary, ManagerId），存储雇员id，雇员名字，雇员薪水和所属经理的id。查询出比所属经理薪水高的雇员名字。
>The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.
>
>| Id | Name  | Salary | ManagerId |
>|:---:|:---:|:---:|:---:|
>| 1 | Joe | 70000  | 3|  
>| 2  | Henry | 80000  | 4         |  
>| 3  | Sam   | 60000  | NULL      |  
>| 4  | Max   | 90000  | NULL      |

## 怎么写的

用到了连接数据表的`join`。

```SQL
select a.name as Employee
from Employee a join Employee b
on a.ManagerId = b.Id
and a.Salary > b.Salary
```
