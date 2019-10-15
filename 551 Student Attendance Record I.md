# 551. Student Attendance Record I

## 题目

学生的考勤记录可分为三种状态： P代表正常考勤，L代表迟到，A代表缺勤。如果一名学生的考勤记录中出现了两次及以上的缺勤或连续三天及以上的迟到则不合格。给出考勤记录，判断学生考勤是否合格。

>You are given a string representing an attendance record for a student. The record only contains the following three characters:
>
> - **'A'** : Absent.
> - **'L'** : Late.
> - **'P'** : Present.
>
>A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).
>
>You need to return whether the student could be rewarded according to his attendance record.
>
>**Example 1:**
>
>>Input: "PPALLP"  
>>Output: True
>
>Example 2:
>
>>Input: "PPALLL"  
>>Output: False

## 解法

水题。时间复杂度O(N)，空间O(1)

```java
public boolean checkRecord(String s) {
        for (int i = 0, aNum = 0; i < s.length(); i++ ){
            if (s.charAt(i) == 'A')
                aNum++;
            if (aNum > 1 || (i< s.length() - 2 && s.charAt(i) == 'L' && s.charAt(i+1) == 'L' && s.charAt(i+2) == 'L'))
                return false;
        }
        return true;
    }
```
