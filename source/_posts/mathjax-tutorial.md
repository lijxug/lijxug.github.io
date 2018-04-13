---
title: How to write equation in my blog
tags:
  - MathJax
  - LaTex
categories:
  - memo
author: Jason Li
date: 2018-04-13 11:02:21
---


# Preface

Thanks to [this blog](https://jdhao.github.io/2018/01/25/hexo-mathjax-equation-number/), I learned to enble MathJax equation numbering in my blog.

However, when I tried to write down equations, it's so confusing that whether I write down the things I want, and it always takes too much time for trial and error. So I decided to record the trials for future references.

<!--more-->

# LaTex Grammer

Inline style: use `$...$` to define inline style latex equation

- code`$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$`
- shown$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$


Display stype: use `$$...$$` to define Display style

Some examples (or test cases):
we have $x\<y$
```
we have $$x\<y$$
```

... when $x &lt; y$ we have ...
```
... when $x &lt; y$ we have ...
```

... when $x \lt y$ we have ...
```
... when $x \lt y$ we have ...
```

$$x+1\over\sqrt{1-x^2} \tag{i}\label{eq_tag}$$

```
$$x+1\over\sqrt{1-x^2} \tag{i}\label{eq_tag}$$
```

$$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$$

```
$$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$$
```

$$\begin{equation}
    \sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t
\end{equation}$$

```
$$\begin{equation}
    \sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t
\end{equation}$$
```

$\alpha$
$$\alpha$$
$$\lim_{x\to 0}$$

```
$\alpha$
$$\alpha$$
$$\lim_{x\to 0}$$
```


#Refernces

- [https://jdhao.github.io/2017/10/06/hexo-markdown-latex-equation/ - to solve MathJax usage problem in Hexo](https://jdhao.github.io/2017/10/06/hexo-markdown-latex-equation/)
- [https://blog.csdn.net/ethmery/article/details/50670297 - for Basic grammer](https://blog.csdn.net/ethmery/article/details/50670297)

