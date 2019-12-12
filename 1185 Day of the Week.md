# 1185. Day of the Week

## 题目

给定年月日，判断这一天是星期几。

>Given a date, return the corresponding day of the week for that date.
>
>The input is given as three integers representing the day, month and year respectively.
>
>Return the answer as one of the following values `{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}.`
>
>**Example 1:**
>
>>Input: day = 31, month = 8, year = 2019  
>>Output: "Saturday"
>>
>**Example 2:**
>
>>Input: day = 18, month = 7, year = 1999  
>>Output: "Sunday"  
>
>**Example 3:**
>
>>Input: day = 15, month = 8, year = 1993  
>>Output: "Sunday"
>
>Constraints:
>
> - The given dates are valid dates between the years 1971 and 2100.

## 解法

没什么骚想法，算总共有多少天呗，1971-2100也就四万多天。

查了查万年历，1971年1月1日是星期五。这就好办了。

```java
public String dayOfTheWeek(int day, int month, int year) {
        //1971-1-1 is Friday.
        String[] dayOfWeek ={"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
        int[] dayInMonth = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        int ret = 0;
        for (int i = 1971; i< year; i++)
            ret += (isLeapYear(i)) ? 366 : 365;
        for (int i = 0; i < month - 1; i++)
            ret += dayInMonth[i];
        if (month > 2 && isLeapYear(year)) ret+=1;
        ret += day - 1;
        return dayOfWeek[(ret + 5) % 7];
    }

    private boolean isLeapYear(int year){
        return ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0));
    }
```
