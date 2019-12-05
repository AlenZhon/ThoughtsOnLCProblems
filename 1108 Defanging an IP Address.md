# 1108. Defanging an IP Address

## 题目

给一个IPV4的地址每个分隔号加上方括号。

>Given a valid (IPv4) IP address, return a defanged version of that IP address.
>
>A defanged IP address replaces every period "." with "[.]".
>
>**Example 1:**
>
>>Input: address = "1.1.1.1"  
>>Output: "1[.]1[.]1[.]1"
>
>**Example 2:**
>
>>Input: address = "255.100.50.0"  
>>Output: "255[.]100[.]50[.]0"
>
>Constraints:
>
> - The given address is a valid IPv4 address.

## 解法

new 一个StringBuilder(address.length() + 6) 完事？

如果不用StringBuilder的话也可以用这个：

```java
public String defangIPaddr(String address) {
        int size = address.length();
        for(int i = 0; i < size; i++) {
            if(address.charAt(i) == '.') {
                address = address.substring(0,i) + "[.]" + address.substring(++i,size);
                size += 2;
            }
        }
        return address;
    }
```
