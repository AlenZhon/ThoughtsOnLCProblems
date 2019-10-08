# 520. Detect Capital

## 题目

判断一个非空单词内大写字母是否满足如下规则之一，满足返回true，否则返回false。

规则1： 所有字母大写。  
规则2： 所有字母小写。  
规则3： 首字母大写，其他字母小写。

## 解法

substring()和equals()方法。

```java
public boolean detectCapitalUse(String word) {
        return word.substring(1).equals(word.substring(1).toLowerCase()) || word.equals(word.toUpperCase());
    }
```

正则表达式：

```java
public boolean detectCapitalUse(String word) {
        return word.matches("[A-Z]*|[a-z]*|[A-Z][a-z]*");
    }
```

然而正则表达式在OJ上的运行时间(9ms)反而比前一种方法慢(2ms)。提交里1ms的方法示例是用的`for`遍历每一个字母。

```java
public boolean detectCapitalUse(String word) {
        int len=word.length();
        if(len==1)
            return true;
        boolean f1=Character.isUpperCase(word.charAt(0));
        boolean f2=Character.isUpperCase(word.charAt(1));
        if(f1&&f2){
            for(int i=2;i<len;i++){
                if(!Character.isUpperCase(word.charAt(i)))
                    return false;
            }
        }
        else if(f1&&!f2){
            for(int i=2;i<len;i++){
                if(Character.isUpperCase(word.charAt(i)))
                    return false;
            }
        }
        else{
            for(int i=1;i<len;i++){
                if(Character.isUpperCase(word.charAt(i)))
                    return false;
            }
        }
        return true;
    }
```
