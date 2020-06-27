---
title: Basic Linux Commands
date: 2020-01-23 19:06:46
tags:
- linux
categories:
- 技术文档 
---

### 1. du -- display disk usage statistics


```bash
du -d 1 -h Documents # -d:depth -h:"human-readable"
du -d 0 -h Documents
```


<!--more-->

### 2. grep -- file pattern searcher

grep stands for “global regular expression print”. It searches files for lines that match a pattern and returns the results. It is case sensitive.

```
grep "Apple" fruit.txt
grep -i "Apple" fruit.txt #-i:case insensitive
grep -R "Apple" ~/Documents/fruit # -R: recursive

```

#### grep regular expression:

\* 表示重复前一个字节0-无穷次

. 表示一定有一个任意字节

^, $， 行首与行尾
```bash

grep -n '^apple' /home/wang/test.c
```

[] 里面无论有多少字节，仅代表一个字节，如：grep -n ‘t[ae]mp’ test.txt

### 3. find

find命令用于：在一个目录（及子目录）中搜索文件，你可以指定一些匹配条件，如按文件名、文件类型、用户甚至是时间戳查找文件。

示例：
```bash
find ~ -name "_config.yml" -print #在 home 目录下查找名 字为"_config.yml" 的文件
find . -size +1000000c -print #在当前目录下查找大于 1M 字节的文件
```
### find 语句形式：

find [path...] [expression]

path: find命令所查找的目录路径。例如用.来表示当前目录，用/来表示系统根目录

expression: “-options [-print -exec -ok ...]”
 
- -print，find命令将匹配的文件输出到标准输出
- -exec，find命令对匹配的文件执行该参数所给出的shell命令。相应命令的形式为'command' {  } \;，注意{   }和\；之间的空格
```bash
#删除文件大小为零的文件
find ./ -size 0 -exec rm {} \;  
#还可以：
rm -i `find ./ -size 0`  
find ./ -size 0 | xargs rm -f &

#为了用ls -l命令列出所匹配到的文件，可以把ls -l命令放在find命令的-exec选项中：
find . -type f -exec ls -l {  } \;
#在/logs目录中查找更改时间在5日以前的文件并删除它们：
find /logs -type f -mtime +5 -exec rm {  } \;
```
- -ok，和-exec的作用相同，只不过以一种更为安全的模式来执行该参数所给出的shell命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行。
```bash
#在当前目录中查找所有文件名以.LOG结尾、更改时间在5日以上的文件，并删除它们，只不过在删除之前先给出提示.
find . -name "*.conf"  -mtime +5 -ok rm {  } \;
```

### -options 

-size n：[c] 查找文件长度为n块的文件，带有c时表示文件长度以字节计

-depth：在查找文件时，首先查找当前目录中的文件，然后再在其子目录中查找。

-type: 查找某一类型的文件，诸如：
- b 块设备文件。
- d 目录。
- c 字符设备文件。
- p 管道文件。
- l 符号链接文件。
- f 普通文件。
```bash
find /etc -type d -print #在/etc目录下查找所有的目录
find . ! -type d –print 在当前目录下查找除目录以外的所有类型的文件
find /etc -type l –print 在/etc目录下查找所有的符号链接文件
```

### find 与 xargs

>find命令配合使用exec和xargs可以使用户对所匹配到的文件执行几乎所有的命令。在使用find命令的-exec选项处理匹配到的文件时， find命令将所有匹配到的文件一起传递给exec执行。但有些系统对能够传递给exec的命令长度有限制，这样在find命令运行几分钟之后，就会出现溢出错误。错误信息通常是“参数列太长”或“参数列溢出”。这就是xargs命令的用处所在，特别是与find命令一起使用。find命令把匹配到的文件传递给xargs命令，而xargs命令每次只获取一部分文件而不是全部，不像-exec选项那样。这样它可以先处理最先获取的一部分文件，然后是下一批，并如此继续下去。

```bash
find . -type f -print | xargs file #查找系统中的每一个普通文件，然后使用xargs命令来测试它们分别属于哪类文件
find / -name "core" -print | xargs echo "" >/tmp/core.log #在整个系统中查找内存信息转储文件(core dump) ，然后把结果保存到/tmp/core.log 文件中：
find . -type f -print | xargs grep "hostname" #用grep命令在所有的普通文件中搜索hostname这个词
find ./ -mtime +3 -print|xargs rm -f –r #删除3天以前的所有东西 （find . -ctime +3 -exec rm -rf {} \;）
find ./ -size 0 | xargs rm -f & #删除文件大小为零的文件
```


### 4. Redirect

```bash
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

### 5. Piping

```
ls -l -> temp
sort record.txt | uniq 
cat sample2.txt | head -7 | tail -5
ls -l | find ./ -type f -name "*.txt" -exec grep "program" {} \;
# ?
```

### 6. &&, ||, (), {}
```
rm ~/Desktop/1.txt || (cd ~/Desktop/;ls -a;echo "fail")
A=1;echo $A;{ A=2; };echo $A 
A=1;echo $A;( A=2; );echo $A 
```

[Reference](https://blog.51cto.com/151wqooo/1174066)

### 7. Special variable -, $\_ …
```
mkdir -p udacity-git-course/new-git-project && cd $_
```
$\_  在此之前执行的命令或者脚本的最后一个参数
```
# Example: 
cp ~/Desktop/1.txt ~/1.txt && rm ~/Desktop/1.txt && echo "success"
rm ~/Desktop/1.txt || echo "fail"
```

### 8. tar

#### Create tar Archive File:

compress and uncompress files
c: Create a new .tar archive file
v: Verbosely show the .tar file progress
f: File name type of the archive file (?)

```bash
tar -cvf all-fruit-06-26-20.tar  dir1/dir2
```
#### Create tar.gz tar.bz2 Archive File:

To create a compressed gzip archive file we use the option as<font color=red>z</font>.  


```bash
# Note : tar.gz and tgz both are similar
tar -cvzf all-fruit-06-26-20.tar.gz dir1/dir2
tar -cvzf all-fruit-06-26-20.tar.tgz dir1/dir2

# Note: tar.bz2 tar.tbz tar.tb2 are similar
tar -cvzf all-fruit-06-26-20.tar.bz2 dir1/dir2
```
#### Untar tar Archive File:

To untar or extract a tar file, just issue following command using option<font color=red>x</font> (extract).

If you want to untar in a different directory then use option as<font color=red>-C</font>(specified directory).

```
# Untar files in Current Directory
tar -xvf all-fruit-06-26-20.tar

# Untar files in specified Directory
tar -xvf all-fruit-06-26-20.tar -C ~/Documents/fruit

# Untar files in tar.gz
tar -xvf all-fruit-06-26-20.tar.gz

# Untar files in tar.bz2
tar -xvf all-fruit-06-26-20.tar.bz2
```

### List Content of tar Archive File:

To list the contents of tar archive file, just run the following command with option <font color=red>t</font> (list content). 
```bash
tar -tvf all-fruit-06-26-20.tar
tar -tvf all-fruit-06-26-20.tar.gz
tar -tvf all-fruit-06-26-20.tar.bz2
```

### zip and unzip
zip: to compress files into a zip archive
unzip: to extract files from a zip archive.

```
# compress
zip -r fruit.zip /dir1/dir2 #-r: Travel the directory structure recursively
zip -q -r fruip.zip * # if we are in the directory

# uncompress
unzip file.zip -d destination_folder

# if the source and destination directories are the same
unzip file.zip
```

### 9. chmod

### 10. 



References:
[Learn basic commands for Linux, a free and open-source operating system that you can make changes to and redistribute.](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners)

[18 Tar Command Examples in Linux](https://www.tecmint.com/18-tar-command-examples-in-linux/)

[linux中强大且常用命令：find、grep by 吴秦](https://www.cnblogs.com/skynet/archive/2010/12/25/1916873.html)

