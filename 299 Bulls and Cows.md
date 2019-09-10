# 299. Bulls and Cows

## 题目

一个猜数游戏。你在心中想一串数字，开始时你的朋友只知道这串数字是几位数。每轮游戏开始时你的朋友对你的数字进行猜测，你给出一个线索，包含着两个信息：位置和数字都相符的数位个数（`bulls`）和数字相符但位置错误的数位个数（`cows`）。编写程序，在给定你和你朋友的数字时，计算bulls和cows的个数并以`xAyB`的形式给出，`A, B`分别指代`bulls, cows`，`x, y`分别为两者个数。

注意两串数字中均可能会有重复数字。

>You are playing the following `Bulls and Cows` game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.
>
>Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows.
>
>Please note that both secret number and friend's guess may contain duplicate digits.
>
>**Example 1:**
>
>>Input: secret = "1807", guess = "7810"
>>Output: "1A3B"
>>Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
>
>**Example 2:**
>>Input: secret = "1123", guess = "0111"
>>Output: "1A1B"
>>Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
>
>Note: You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

## 解法

想法比较直接。遍历每个数位，如果两数相等就自增`bulls`。对于`cows`，用两个0-9位的数组`numsg, numgs`分别记录每个数位出现的个数。如果在secret number中出现则`numsg`的对应位不为0，只查看此情况。
由于可能有重复数位，如以下测试例：

> secret: 1122 guess: 2211  
> secret: 1134 guess: 0001  
> secret: 1123 guess: 0111  

第一个例子，`numsg[1] = numgs[1] = 2, numsg[2] = numgs[2] = 2`，要求输出`0A4B` 也就是`4 = 2+2 = numsg[1]+numsg[2]`。  
第二个例子，`numsg[1] = 2, numgs[1] = 1`，要求输出`0A1B`，也就是`1 =  numgs[1]`。  
第三个例子，`numsg[1] = 2, numgs[1]= 3`，要求输出`1A1B`，也就是`1 = numsg[1]`

综上， `cows+= Math.min(numsg[i], numgs[i]);`

```java
 public String getHint(String secret, String guess) {
        int[] numsg = new int[10];
        int[] numgs = new int[10];
        int bulls = 0 , cows = 0;
        for (int i = 0 ; i< secret.length(); i++){
            int s = secret.charAt(i) - '0';
            int g = guess.charAt(i) - '0';
            if (s == g) bulls++;
            else {
                numsg[s]++;
                numgs[g]++;
            }
        }
        for (int i =0; i<10; i++)
            if (numsg[i] !=0)
                cows+= Math.min(numsg[i], numgs[i]);
        return bulls + "A" + cows + "B";
    }
```

进一步地，可以将两个数组合成一个，并通过one-pass完成任务。

```java
public String getHint(String secret, String guess) {
    int bulls = 0;
    int cows = 0;
    int[] numbers = new int[10];
    for (int i = 0; i<secret.length(); i++) {
        if (secret.charAt(i) == guess.charAt(i)) bulls++;
        else {
            if (numbers[secret.charAt(i)-'0']++ < 0) cows++;
            if (numbers[guess.charAt(i)-'0']-- > 0) cows++;
        }
    }
    return bulls + "A" + cows + "B";
}
```
