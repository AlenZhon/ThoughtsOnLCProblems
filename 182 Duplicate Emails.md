# 182. Duplicate Emails

## 题目描述

Person数据表中有(Id, email)字段，查询其中重复的email。

>Write a SQL query to find all duplicate emails in a table named Person.
>
>| Id | Email   |
>|:-:|:-:|
>| 1  | a@b.com |
>| 2  | c@d.com |
>| 3  | a@b.com |
>
>For example, your query should return the >following for the above table:
>
>| Email   |
>|:-:|
>| a@b.com |

## 怎么写的

还是用的数据表自连接。

```SQL
select distinct p1.email
from Person p1, Person p2
on p1.Id != p2.Id and p1.email = p2.email;
```

提交之后看solution使用的是`group by`。

```SQL
SELECT Email
FROM PERSON
GROUP BY Email
HAVING COUNT(1) > 1;
```
