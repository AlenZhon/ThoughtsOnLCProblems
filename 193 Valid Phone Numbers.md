# 193. Valid Phone Numbers

## 题目

给定一个file.txt，里面每行是一个电话号码。用bash脚本判断并输出所有正确的电话号码。

>Given a text file file.txt that contains list of phone numbers (one per line), write a one liner bash script to print all valid phone numbers.
>
>You may assume that a valid phone number must appear in one of the following two formats: (xxx) xxx-xxxx or xxx-xxx-xxxx. (x means a digit)
>
>You may also assume each line in the text file must not contain leading or trailing white spaces.
>
>Example:
>
>Assume that file.txt has the following >content:
>
>>987-123-4567  
>>123 456 7890  
>>(123) 456-7890  
>
>Your script should output the following valid phone numbers:
>
>>987-123-4567  
>>(123) 456-7890

## 怎么写

首先肯定是要写出这两种电话号码的正则了。  
`^([0-9]{3}-|\([0-9]{3}\) )[0-9]{3}-[0-9]{4}$`

用`sed`：

```bash
sed -n -r '/^([0-9]{3}-|\([0-9]{3}\) )[0-9]{3}-[0-9]{4}$/p' file.txt
```

`grep`:

```bash
grep -P '^(\d{3}-|\(\d{3}\) )\d{3}-\d{4}$' file.txt
```
