---
title: Markdown Basics
date: 2019-07-15 09:53:58
tags:
- markdown
categories:
- 技术文档
mathjax: true
type: "picture"
---

## Headers

### h3
#### h4
##### h5

```
### h3
#### h4
##### h5
```

## Horizontal rules
---

```markdown
---
```

## Italics, Bold

_Hello_
**Hello**
~~Hello~~

```
_Hello_
**Hello**
~~Hello~~
```

<!--more-->

## Image  

```markdown
![alt text](http://path/to/img.jpg "Title")
<img src="http://path/to/img.jpg" alt="alt text" title="Title" />
```
Group Pictures:
{% gp 3-1 %}
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
{% endgp %}


```markdown
<% gp 3-1 %>
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
<img width=99.75% src=https://i.loli.net/2020/02/22/e85NALZaliucnsG.jpg />
<% endgp %>

```
Linking Images

```markdown
[<img width= 30% src=https://i.loli.net/2020/06/27/k3puFt1SbBLzv9i.jpg />](https://meng05.github.io/2020/03/31/osprey-back/)
```
[<img width= 30% src=https://i.loli.net/2020/06/27/k3puFt1SbBLzv9i.jpg />](https://meng05.github.io/2020/03/31/osprey-back/)

## Code 

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

## Lists

### unordered List
- line1
  -line1.1(2 blank space)
  - line1.2
- line2
- line3

```markdown
- line1
  -line1.1(2 blank space)
  - line1.2
- line2
- line3
```

### Ordered List
1. line1
   1.1 line1.1 （3 blank space）
   1.2 line1.2
2. line2
3. line3

```markdown
1. line1
   1.1 line1.1 （3 blank space）
   1.2 line1.2
2. line2
3. line3
```
## Table

colname|colname|colname
--|---|---
Lucy|15|apple

```markdown
colname|colname|colname
--|---|---
Lucy|15|apple
```
## Math

$$\frac{x_1^2+x_2^2}{3}$$
$$\sum_{k=1}^n\frac{1}{k}$$
$$\int_a^b f(x)dx$$
$$E=mc^2$$

```markdown
$$\frac{x_1^2+x_2^2}{3}$$
$$\sum_{k=1}^n\frac{1}{k}$$
$$\int_a^b f(x)dx$$
$$E=mc^2$$
```
## Escaping Backticks 

```markdown
\\ 
\` 
\* 
\_ 
\{} 
\[] 
\() 
\# 
\+ 
\- 
\. 
\! 
```
##  URLs and Email Addresses

```markdown
<https://meng05.github.io>

<zhangsan@example.com>
```
The rended output looks like this:

<https://meng05.github.io>

<zhangsan@example.com>

## Adding Title and Formatting Links

This is my personal website **[屋顶上的老斑鸠](https://meng05.github.io/)**
This is about *[Turkey Vulture](https://meng05.github.io/2020/02/17/Turkey-Vulture/)*

```markdown
This is my personal website **[屋顶上的老斑鸠](https://meng05.github.io/)**
This is about *[Turkey Vulture](https://meng05.github.io/2020/02/17/Turkey-Vulture/)*
```

## Reference-sytle Links
?


## Blockquotes

Blockquotes can contain multiple paragraphs. Add a > on the blank lines between the paragraphs.

>Tomorrow is another day!
>
>Today is a good day!

```markdown
>Tomorrow is another day!
>
>Today is a good day!
```

Nested Blockquotes:
> Tomorrow is another day!
>
>> Today is a good day!

```markdown
> Tomorrow is another day!
>
>> Today is a good day!
```

## References:

<https://www.markdownguide.org/basic-syntax/#links>
