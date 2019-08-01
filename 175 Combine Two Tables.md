# 175. Combine Two Tables

## 题目描述

```SQL
Create table Person (PersonId int, FirstName varchar(255), LastName varchar(255))
Create table Address (AddressId int, PersonId int, City varchar(255), State varchar(255))
Truncate table Person
insert into Person (PersonId, LastName, FirstName) values ('1', 'Wang', 'Allen')
Truncate table Address
insert into Address (AddressId, PersonId, City, State) values ('1', '2', 'New York City', 'New York')
```

>Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:
>
>FirstName, LastName, City, State

## 怎么写的

（突如其来的SQL闪到我的眼了）

>**Algorithm**
>
>Since the PersonId in table Address is the foreign key of table Person, we can join this two table to get the address information of a person.
>
>Considering there might not be an address information for every person, we should use `outer join` instead of the default `inner join`.
>
>**MySQL**
>
>```SQL
>select FirstName, LastName, City, State
>from Person left join Address
>on Person.PersonId = Address.PersonId;
>```
>
>>Note: Using `where` clause to filter the records will fail if there is no address information for a person because it will not display the name information.
