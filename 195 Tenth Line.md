# 195 Tenth Line

## 题目描述

>Given a text file file.txt, print just the 10th line of the file.
>
>**Example:**
>
>Assume that file.txt has the following content:
>>
>>Line 1  
>>Line 2  
>>Line 3  
>>Line 4  
>>Line 5  
>>Line 6  
>>Line 7  
>>Line 8  
>>Line 9  
>>Line 10  
>
>Your script should output the tenth line, which is:
>
>>Line 10
>
>**Note:**
>
>1. If the file contains less than 10 lines, what should you output?
>2. There's at least three different solutions. Try to explore all possibilities.

## 怎么写的

现场查了一下bash语言的`while cat if break`怎么写。

```bash
filename="file.txt"
count=0
cat $filename | while read line
do
 let "count++"
 if [ $count == 10 ]
 then
    echo $line
    break
 fi
done
```

写得简单一点那就是

```bash
count=0
while (( i++ < 10 ))
do
  read line
done < file.txt
echo $line
```

其他解法如下：

```bash
# Solution 2
# awk是一种处理文本文件的语言，是一个强大的文本分析工具。
awk 'FNR == 10 {print }'  file.txt
# OR
awk 'NR == 10' file.txt

# Solution 3
sed -n 10p file.txt
# sed 可依照脚本的指令来处理、编辑文本文件
# -n或--quiet或--silent 仅显示script处理后的结果。
# p ：打印，亦即将某个选择的数据印出。

# Solution 4
tail -n+10 file.txt|head -1
# tail 命令可用于查看文件的内容，有一个常用的参数 -f 常用于查阅正在改变的日志文件。

```
