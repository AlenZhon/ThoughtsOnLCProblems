# 66 Plus One

## 题目描述

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

## 怎么解的

主要就是考虑进位的问题了。由于只是给整个数加一，进位最复杂的情况即为类似999进位到1000，需要在数组中多加一位。

一个从数列尾部开始的for循环，如果当前元素不是9则加一return，否则就置零。如果最后还没return那么就需要重新安排一个数列，存放多进出来的那个1。
