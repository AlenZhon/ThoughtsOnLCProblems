# 1154. Day of the Year

## 题目

给定一个日期字符串格式为"YYYY-MM-DD"分别代表年月日，计算该日期是当年的第几天。

字符串长度固定为10。日期范围从1900年1月1日到2019年12月31日。

>Given a string date representing a Gregorian calendar date formatted as YYYY-MM-DD, return the day number of the year.
>
>**Example 1:**
>
>>Input: date = "2019-01-09"  
>>Output: 9
>>Explanation: Given date is the 9th day of the year in 2019.
>
>**Example 2:**
>
>>Input: date = "2019-02-10"  
>>Output: 41  
>
>**Example 3:**
>
>>Input: date = "2003-03-01"  
>>Output: 60  
>
>**Example 4:**
>
>>Input: date = "2004-03-01"  
>>Output: 61
>
>**Constraints:**
>
> - date.length == 10
> - date[4] == date[7] == '-', and all other date[i]'s are digits
> - date represents a calendar date between Jan 1st, 1900 and Dec 31, 2019.

## 解法

自信题目。判断一下是否是闰年，初始化一个数组存储每个月有多少天即可。

```java
public int dayOfYear(String date) {
        int year = Integer.valueOf(date.substring(0, 4)),
            month = Integer.valueOf(date.substring(5, 7)),
            day = Integer.valueOf(date.substring(8));
        int[] dayInMonth = new int[]{31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        int ret = 0;
        for (int i = 0; i< month - 1; i++)
            ret += dayInMonth[i];
        ret += day;
        if (isLeapYear(year) && month > 2) ret+=1;
        return ret;
    }
    private boolean isLeapYear(int year){
        return ((year % 100 != 0 && year % 4 == 0) || (year % 400 == 0));
    }
```
