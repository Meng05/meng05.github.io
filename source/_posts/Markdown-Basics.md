---
title: Markdown Basics
date: 2019-07-15 09:53:58
tags:
- markdown
- Study Note
categories:
- Tech
mathjax: true
type: "picture"
---
这是一篇测试Markdown语法的文章.
<!--more-->

## 一、标题

### h3
#### h4
##### h5
###### h6

```
### h3
#### h4
##### h5
###### h6
```

## 二、分割线
---

```
---
```

## 三、 引用

这里是引用

> 这里是引用


## 四、常见字体样式

_斜体_
**粗体**
~~删除线~~

```
_斜体_
**粗体**
~~删除线~~
```

## 五、图片
测试图片
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
调整图片大小
<img width="50%" alt="moon" src="https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg">

```
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
<img width="50%" alt="moon" src="https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg">
```
多图显示
{% gp 3-1 %}
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
{% endgp %}
```
{% gp 3-1 %}
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
![moon](https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg)
{% endgp %}
```

## 六、 代码行与代码块

代码块：
```cpp
int i;
for (i=1; i<=9; i++)
{
    cout << i*i << endl;
}
```

````
```cpp
int i;
for (i=1; i<=9; i++)
{
    cout << i*i << endl;
}
```
````

## 七、超链接
[github](http://github.com)
```
[github](http://github.com)
```

## 八、 列表
### 无序列表
- 项目1
  -项目1.1(缩进2空格)
  - 项目1.2
- 项目2
- 项目3
```
- 项目1
  -项目1.1(缩进2空格)
  - 项目1.2
- 项目2
- 项目3
```

### 有序列表
1. 项目1
   1.1 项目1.1 （缩进3空格）
   1.2 项目1.2
2. 项目2
3. 项目3
```
1. 项目1
   1.1 项目1.1 （缩进3空格）
   1.2 项目1.2
2. 项目2
3. 项目3
```
## 九、 表格

表头|表头|表头
--|---|---
张三|李四|王五
```
表头|表头|表头
--|---|---
张三|李四|王五
```
## 十、数学公式
$$\frac{x_1^2+x_2^2}{3}$$
$$\sum_{k=1}^n\frac{1}{k}$$
$$\int_a^b f(x)dx$$
$$E=mc^2$$

```
$$\frac{x_1^2+x_2^2}{3}$$
$$\sum_{k=1}^n\frac{1}{k}$$
$$\int_a^b f(x)dx$$
$$E=mc^2$$
```
## 十一、转义
可转义的有：
```
\\ 反斜杠
\` 反引号
\* 星号
\_ 下划线
\{} 大括号
\[] 中括号
\() 小括号
\# 井号
\+ 加号
\- 减号
\. 英文句号
\! 感叹号
```



## References:
[TMaize Blog - 主题预览](http://blog.tmaize.net/posts/2015/01/01/%E4%B8%BB%E9%A2%98%E9%A2%84%E8%A7%88.html)
