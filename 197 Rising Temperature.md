# 197. Rising Temperature

## 题目

>Given a `Weather` table, write a SQL query to find all dates' Ids with higher temperature compared to its previous (yesterday's) dates.
>
>| Id(INT) | RecordDate(DATE) | Temperature(INT) |
>|:-:|:-:|:-:|
>|       1 |       2015-01-01 |               10 |
>|       2 |       2015-01-02 |               25 |
>|       3 |       2015-01-03 |               20 |
>|       4 |       2015-01-04 |               30 |
>
>For example, return the following Ids for the above `Weather` table:
>
>| Id |
>|:-:|
>|  2 |
>|  4 |

## 怎么写的

不懂MySQL里怎么作差，看了一眼solution说有个`DATEDIFF(exp1,exp2)`可以计算两个日期之间的差值。

>`DATEDIFF(expr1,expr2)`
>
>`DATEDIFF()` returns `expr1 − expr2` expressed as a value in days from one date to the other. `expr1` and `expr2` are date or date-and-time expressions. Only the date parts of the values are used in the calculation.

```SQL
select w2.Id from Weather w1, Weather w2
where w2.Temperature > w1.Temperature and DATEDIFF(w2.RecordDate, w1.RecordDate) =1
```
