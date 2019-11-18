# 929. Unique Email Addresses

## 题目

电子邮箱地址的格式为`local name + @ + domain name`。在local name中，如果加入了英文句号( . )，邮箱将自动忽略句号。如果加入了加号( + )，邮箱将自动忽略加号及之后的内容。（这两条规则不适用于domain name。）现在一个数组中给定一些邮箱地址，向每个邮箱地址发送一封邮件。判断最后有多少个真实的地址收到了邮件？

>Every email consists of a local name and a domain name, separated by the @ sign.
>
>For example, in alice@leetcode.com, alice is the local name, and leetcode.com is the domain name.
>
>Besides lowercase letters, these emails may contain '.'s or '+'s.
>
>If you add periods ('.') between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, "alice.z@leetcode.com" and "alicez@leetcode.com" forward to the same email address.  (Note that this rule does not apply for domain names.)
>
>If you add a plus ('+') in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example m.y+name@email.com will be forwarded to my@email.com.  (Again, this rule does not apply for domain names.)
>
>It is possible to use both of these rules at the same time.
>
>Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails?
>
>**Example 1:**
>
>>Input: [`"test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"`]  
>>Output: 2  
>>Explanation: `"testemail@leetcode.com"` and `"testemail@lee.tcode.com"` actually receive mails.
>
>**Note:**
>
> - `1 <= emails[i].length <= 100`
> - `1 <= emails.length <= 100`
> - Each `emails[i]` contains exactly one '@' character.
> - All local and domain names are non-empty.
> - Local names do not start with a '+' character.

## 解法

用了一大堆String类里的方法。

```java
public int numUniqueEmails(String[] emails) {
        HashSet<String> set = new HashSet<>();
        for (String email : emails) {
            int i = email.indexOf("@");
            String local = email.substring(0, i);
            String domain = email.substring(i);
            if (local.indexOf("+") > 0)
                local = local.substring(0, local.indexOf("+"));
            set.add(local.replaceAll("\\.","") + domain);
        }
        return set.size();
    }
```

值得注意的是， `.replaceAll()`方法中的第一个参数必须写成`"\\."`才能表示英文句号。如果单用`"."`则会按照正则表达式的规则将`"."`作为任意字符通配符进行正则匹配。

大佬们选择了自己写函数进行判断。

```java
public static int numUniqueEmails(String[] emails) {

    Set<String> processed = new HashSet();

    int len = emails.length;
    for (int i = 0; i < len; i++)
      processed.add(process(emails[i].toCharArray()));

  return processed.size();
}

public static String process(char[] email) {

    int len = email.length;
    char[] res = new char[len];
    int numOfLetters = 0;

    boolean skipCharacters = false;
    boolean atOccured = false;
    for (int i = 0; i < len; i++) {
        char c = email[i];
        if ( !atOccured && c == '.') {
            continue;
        } else if (!atOccured && c == '+' ) {
            skipCharacters = true;
            continue;
        } else if (c == '@') {
            atOccured = true;
            skipCharacters = false;
        }

        if (!skipCharacters) {
            res[numOfLetters++] = c;
        }

    }

    return new String(res, 0, numOfLetters);
}
```
