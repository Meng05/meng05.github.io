---
title: Linux Command Line Basics
date: 2020-01-23 19:06:46
tags:
- Study Note
- linux
categories:
- Tech
---

这是一篇关于 Linux Command Line Basics学习笔记。
<!--more-->

## 查看文件大小
du (disk usage)

-h 以K、M、G人性化的方式显示

-a 显示文件和目录

–max-depth=n 如n=0不深入到子目录

## 查找之grep
查找并把匹配的行打印出来

-r 递归查找文件的子文件，如果有的话

-n 显示打到位置的行号

-i 不考虑大小写

-v 反向查找。显示不包含的位置。

grep
```
grep -rn "地图" 
```

grep 与正则表达式

重复字节* 表示重复前一个字节0-无穷次

任意一个字节. 表示一定有一个任意字节

行首与行尾^, $， 如：grep -n ‘^d’ /home/wang/test.c

[]里无论有多少字节，仅代表一个字节，如：grep -n ‘t[ae]mp’ test.txt


## Redirect
```
# Examples
ls -al > listings
# >> To add more content to the existing file
Mail -s "Subject" to-address < Filename
# ERROR Rediction
myprogram 2>errorsfile
find . -name 'my*' 2>error.log
ls Documents ABC> dirlist 2>&1
$ cat result.txt | grep "Rajat Dua" | tee file2.txt | wc -l
```
[References](https://www.guru99.com/linux-redirection.html)

## Piping
```
ls -l -> temp
sort record.txt | uniq 
cat sample2.txt | head -7 | tail -5
ls -l | find ./ -type f -name "*.txt" -exec grep "program" {} \;
# ?
```

##  &&, ||, (), {}
```
rm ~/Desktop/1.txt || (cd ~/Desktop/;ls -a;echo "fail")
A=1;echo $A;{ A=2; };echo $A 
A=1;echo $A;( A=2; );echo $A 
```

[Reference](https://blog.51cto.com/151wqooo/1174066)

## Special variable -, $_ …
```
mkdir -p udacity-git-course/new-git-project && cd $_
```
$_  在此之前执行的命令或者脚本的最后一个参数
```
# Example: 
cp ~/Desktop/1.txt ~/1.txt && rm ~/Desktop/1.txt && echo "success"
rm ~/Desktop/1.txt || echo "fail"
```
## 查看文件大小
