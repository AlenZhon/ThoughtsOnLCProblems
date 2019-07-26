# 137. Single Number II

## 题目描述

给定非空数组，数组元素除了一个元素只出现了一次，其他元素均出现三次。找出那个单独的元素。尝试设计一个不使用extra memory的算法。

>Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.
>
>**Note:**
>
>Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
>
>Example 1:
>
>>**Input:** [2,2,3,2]
>>**Output:** 3
>
>Example 2:
>
>>**Input:** [0,1,0,1,0,1,99]
>>**Output:** 99

## 怎么想的

回想#136 Single Number使用异或运算，是因为它具备如下性质：  

- A^B = B^A
- A^B^B = A

那么这题需要找到一种类似的运算，使得它具备如下性质：

- 交换律 F(A,B) = F(B,A)
- F(A,B,B,B) = A

想构造一个逻辑函数式表示F()，然而划拉了很久草稿纸失败了，放弃思考.jpg。如果做出一个三进制就好了（脑洞）。

运行时间0ms解法如下：

```java
 public int singleNumber(int[] nums) {
    int ones = 0, twos = 0;
    for(int i = 0; i < nums.length; i++){
        ones = (ones ^ nums[i]) & ~twos;
        twos = (twos ^ nums[i]) & ~ones;
    }
    return ones;
}
```

>What we need to do is to store the number of '1's of every bit. Since each of the 32 bits follow the same rules, we just need to consider 1 bit. We know a number appears 3 times at most, so we need 2 bits to store that. Now we have 4 state, 00, 01, 10 and 11, but we only need 3 of them.
>
>In this solution, 00, 01 and 10 are chosen. Let 'ones' represents the first bit, 'twos' represents the second bit. Then we need to set rules for 'ones' and 'twos' so that they act as we hopes. The complete loop is 00->10->01->00(0->1->2->3/0).
>
> - For 'ones', we can get `ones = ones ^ A[i];` `if (twos == 1) then ones = 0`, that can be tansformed to `ones = (ones ^ A[i]) & ~twos`.
>
> - Similarly, for 'twos', we can get `twos = twos ^ A[i]; if (ones* == 1) then twos = 0` and `twos = (twos ^ A[i]) & ~ones`. Notice that 'ones*' is the value of 'ones' after calculation, that is why twos is calculated later.

## 八仙过海的评论区解法

看了Discussion区，不禁感叹那是真滴牛皮。

- 评论区其中一位大神便使用了真值表进行逻辑函数的运算。**这个方法核心思想是建立一个记录状态的变量**，此方法适用于其他所有元素出现K次，求唯一一个元素出现M次的问题（every one occurs K times except one occurs M times）。对于此问题，K=3，M=1。

```java
public int singleNumber(int[] nums) {
        //we need to implement a tree-time counter(base 3) that if a bit appears three time ,it will be zero.
        //#curent  income  ouput
        //# ab      c/c       ab/ab
        //# 00      1/0       01/00
        //# 01      1/0       10/01
        //# 10      1/0       00/10
        // a=~abc+a~b~c;
        // b=~a~bc+~ab~c;
        int a=0;
        int b=0;
        for(int c:nums){
            int ta=(~a&b&c)|(a&~b&~c);
            b=(~a&~b&c)|(~a&b&~c);
            a=ta;
        }
        //we need find the number that is 01,10 => 1, 00 => 0.
        return a|b;
    }
```

- 另一位大神构造了一个32bit位的int，从**比较所有元素的每一位**入手，每当有三个元素在这一位上均为1则清零。最后留下的便是单独的那个元素。（这个思想和三进制的想法不谋而合，非常阔以）。方法时间复杂度为O(32n)，并且容易扩展到其他所有元素出现K次，唯一一个元素出现1次的问题。

> I like to think about the number in 32 bits and just count how many 1s are there in each bit, and `sum %= 3` will clear it once it reaches 3. After running for all the numbers for each bit, if we have a 1, then that 1 belongs to the single number, we can simply move it back to its spot by doing `ans |= sum << i;`
>
>This has complexity of O(32n), which is essentially O(n) and very easy to think and implement. Plus, you get a general solution for any times of occurrence. Say all the numbers have 5 times, just do `sum %= 5`.

```java
public int singleNumber(int[] nums) {
    int ans = 0;
    for(int i = 0; i < 32; i++) {
        int sum = 0;
        for(int j = 0; j < nums.length; j++) {
            if(((nums[j] >> i) & 1) == 1) {
                sum++;
                sum %= 3;
            }
        }
        if(sum != 0) {
            ans |= sum << i;
        }
    }
    return ans;
}
```
