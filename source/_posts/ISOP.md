---
title: >-
  Note: Isoform-level gene expression patterns in single-cell RNA-sequencing
  data
tags:
  - AS
  - single-cell
  - RNA-sequencing
categories:
  - note
Author: Jason Li
date: 2018-05-06 13:56:00
---


<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Abstract
这篇文章早在2016年就在bioRxiv上online了，但是一直到今年才在bioinformatics上发出来。
文章主要贡献是通过混合模型描述了单细胞的isoform的表达pattern。算是比较少的对单细胞RNAseq isoform level进行描述。

<!--more-->

在这篇文章里作者介绍了一种方法，ISOform-Patterns(ISOP), 来分析并且分类单细胞的isoform基因表达量数据。 
主要提出了同一个基因下不同isoform的6种表达模式。 
为了得到系统性的对单细胞isoform表达 pattern 进行分类， 作者在在一个乳腺癌细胞系(MDA-MB-231; N=327 cells)上进行了尝试并且在其他三个数据集上进行了重复(?)。
作者随后评估了单细胞的随机性对这些pattern产生所造成的影响， 并且阐释了ISOP如何能够用来分析差异性的isoform pattern。
最后作者用一个模拟数据集测试了ISOP方法。

# 作者信息
暂无

# Introduction
pass 

# Method

使用高斯混合模型对于一个细胞$i$表达的一个基因$j$的一对isoforms$\\{a, b\\}$而言，log变换后的表达量$\Delta_{i,j,a,b}$ $\eqref{eq1}$ 进行拟合$\eqref{eq2}, \eqref{eq3}$。
$y_{i,j,a}$ 和 $y_{i,j,b}$ 代表的是isoform $a$和$b$ 在细胞$i$里的log表达量。
参数$w_k$是混合的$k$ component权重，$K$是总component数。作者把$K$限制到 $\leq 3$。

$\eqref{eq2}, \eqref{eq3}$ 的








>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！