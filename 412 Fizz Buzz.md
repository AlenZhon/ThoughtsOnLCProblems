# 412. Fizz Buzz

## 题目

输出[1,n]的`list<String>`，要求3的倍数替换为`Fizz`，5的倍数替换为`Buzz`，同时是3和5的倍数被替换为`FizzBuzz`。

>Write a program that outputs the string representation of numbers from 1 to n.
>
>But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.
>
>**Example:**
>
>>n = 15,
>>
>>Return:
>>["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]

## 解法

直接写啊。时间复杂度O(N)，由于除了输出的数列没有新的数据结构要安排，所以空间复杂度O(1)。
