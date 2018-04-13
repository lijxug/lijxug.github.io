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
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Preface

Thanks to [this blog](https://jdhao.github.io/2018/01/25/hexo-mathjax-equation-number/), I learned to enble MathJax equation numbering in my blog.

However, when I tried to write down equations, it's so confusing that whether I write down the things I want, and it always takes too much time for trial and error. So I decided to record the trials for future references.

<!--more-->

# LaTex Grammer

## Basic
Inline style: use `$...$` to define inline style latex equation

- code`$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$`
- show$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$

Display stype: use `$$...$$` to define Display style

- code`$$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$$`
- show$$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$$

## Greak letter

For all letter, check [this post](https://blog.csdn.net/ethmery/article/details/50670297).

`$\alpha$` => $\alpha$
`$\beta$` => $\beta$
`$\delta$` => $\delta$
`$\theta$` => $\theta$
`$\mu$` => $\mu$
`$\pi$` => $\pi$
`$\chi$` => $\chi$
`$\epsilon$` => $\epsilon$

...

Capital:
`$\Gamma$` => $\Gamma$
*italic*:
`$\varGamma$` => $\varGamma$

## Letter modifier

### super/sub-script
- superscript: `^`
- subscript: `_`
- example: `$C_n^2$` => $C_n^2$

### Vector
- `$\vec a$` => $\vec a$
- `$\overrightarrow{xy}$` => $\overrightarrow{xy}$

### Group
- `${}$` 
- example: `$10^{10}$` => $10^{10}$ ; `$10^10$` => $10^10$

### Bracket
- `$()$` => $()$
- `$[]$` => $[]$
- `$\\{\\}` => $\\{\\}$

>因为 Markdown 文件的处理实际上经过两个步骤，首先 Markdown 引擎把 Markdown 变为 html 文件, 然后 MathJax 再负责解释其中的数学公式。 第一步中，由于 backslash 在 Markdown 属于特殊字符，用来转义，所以两个 backslash 经过 Markdown 引擎处理，只剩下一个，等到 MathJax 引擎处理时，实际上只有一个 backslash，MathJax 把它当作 LaTeX 中的空格>

- `$(\frac{x}{y})$` => $(\frac{x}{y})$
- `$\left(\frac{x}{y}\right)$` => $\left(\frac{x}{y}\right)$

### sum/lim/integral/fraction/radical
- `$\sum_{i=1}^n{a_i}$` => $\sum_{i=1}^n{a_i}$
- `$\lim_{x\to 0}{(X+1)}$` => $\lim_{x\to 0}{(X+1)}$
- `$\int_0^\infty{fxdx}$` => $\int_0^\infty{fxdx}$
- `$\frac{formula1}{formula2}$` => $\frac{formula1}{formula2}$
- `$\sqrt[x]{y}$` => $\sqrt[x]{y}$

### Function
- `$\function(x)$` => $\function(x)$
- examples: `$\sin x$` => $\sin x$, `$\ln x$` => $ln x$, `$\max(a,b,c)$` => $\max(a,b,c)$

### Special symbol
| code | show |
|:-:|:-:|
|`$\infty$`|$\infty$|
|`$\cup$`|$\cup$|
|`$\cap$`|$\cap$|
|`$\subset$`|$\subset$|
|`$\subseteq$`|$\subseteq$|
|`$\supset$`|$\supset$|
|`$\in$`|$\in$|
|`$\notin$`|$\notin$|
|`$\varnothing$`|$\varnothing$|
|`$\forall$`|$\forall$|
|`$\exists$`|$\exists$|
|`$\lnot$`|$\lnot$|
|`$\nabla$`|$\nabla$|
|`$\partial$`|$\partial$|

### Spaces

- LaTex will ignore any spaces in the code
- `$a\ b$` => $a\ b$
- `$a\quad b` => $a\quad b$

### Other examples (or test cases):

`$x<y$` => $x<y$
`$x=y$` => $x=y$
`$x\leq y$` => $x\leq y$
`$x\neq y$` => $x\neq y$
`$x\geq y$` => $x\geq y$

### Equation number

Thanks to [the post here](https://jdhao.github.io/2018/01/25/hexo-mathjax-equation-number/).

Since I deploy this blog using Travis, it's more easier for me to choose the first way ... according to the post above.

>According to MathJax official documentation, just paste the following script into the front of your Markdown file,

```
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>
```


```
$$\begin{equation}
e=mc^2
\end{equation}\label{eq1}$$
```

$\downarrow$ (`$\downarrow$`)

$$\begin{equation}
e=mc^2
\end{equation}\label{eq1}$$

```
$$\begin{equation}
\begin{aligned}
a &= b + c \\\\
  &= d + e + f + g \\\\
  &= h + i
\end{aligned}
\end{equation}\label{eq2}$$
```

$\downarrow$ 

$$\begin{equation}
\begin{aligned}
a &= b + c \\\\
  &= d + e + f + g \\\\
  &= h + i
\end{aligned}
\end{equation}\label{eq2}$$

## reference equation

for the equations below:
```
$$\begin{align}
a &= b + c \label{eq3} \\\\
x &= yz \label{eq4}\\\\
l &= m - n \label{eq5}
\end{align}$$
```

$\downarrow$

$$\begin{align}
a &= b + c \label{eq3} \\\\
x &= yz \label{eq4}\\\\
l &= m - n \label{eq5}
\end{align}$$

You can use `$\eqref{eq3}$` to refer to equation $\eqref{eq3}$, which is the same for $\eqref{eq4}$ and $\eqref{eq5}$.

### to be continued: Matrix

# References

- [https://jdhao.github.io/2017/10/06/hexo-markdown-latex-equation/ - to solve MathJax usage problem in Hexo](https://jdhao.github.io/2017/10/06/hexo-markdown-latex-equation/)
- [https://blog.csdn.net/ethmery/article/details/50670297 - for Basic grammer](https://blog.csdn.net/ethmery/article/details/50670297)

>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！