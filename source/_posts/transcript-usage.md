---
title: 'The current knowledge of the concept: (Differential) Transcript Usage'
tags:
  - single-cell
  - Transcript-usage
  - AS
categories:
  - note
author: Jason Li
date: 2018-03-26 21:35:23
---


### Preface

了解一下目前学术界对于某个基因在不同条件下使用不同transcripts这个概念的定义、了解程度和研究内容。


<!--more-->

### Articles

总共找到这么几篇，先简单看这么多，以后有空再加吧

---

[Isoform prefiltering improves performance of count-based methods for analysis of differential transcript usage](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4729156/ "Genome Biology*, 2016 / BioRxiv, 2015")

[Post of it on RNA-seq blog](http://www.rna-seqblog.com/differential-transcript-usage-from-rna-seq-data-isoform-pre-filtering-improves-performance-of-count-based-methods/) 在2015年是这么评价这篇文章的：
RNA-seq使针对转录组的定量研究成为可能，其中一个全新的应用就是探索在不同实验条件下的转录本的使用变化。
当时有这么几种方法可以来揭示这种变化(即differential transcript usage, DTU)，例如基于注释的外显子层面的计数(annotation-based exon-level counting)， [PSI](#PSI)的差异分析(Differential analysis of PSI)， 或者直接定量拼装好的transcripts(quantitative analysis of assembled transcripts)。

University of Zurich 的研究者们比较了当时最先进的办法，并且提出了对常用workflow的一些改进。
他们使用模拟数据评估了传统工作流程的效果。
并且探索了一下使用非标准的计数矩阵（??原文是non-standard counting bin， 可能是一个基于exon的计数方案）作为DEXSeq输入的效果。

他们发现，虽然传统的计数矩阵整体上来看效果最好，但一些非传统的方案在某些特殊的领域表现更佳(仿佛是一句废话)。
并且发现大多数基于技术的方法比基于事件和组装做估计的方法都要好。另一方面，研究者发现如果注释不完全可能会造成对DTU估计不准确。此时如果预先filter掉那些isoform可以提升FDR control。

![](http://www.rna-seqblog.com/wp-content/uploads/2015/08/isoform.png)

简单看一下文章里面对DTU的背景介绍部分，

![GB,2016 Fig1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4729156/bin/13059_2015_862_Fig1_HTML.jpg)
Fig1 简单介绍了一下DTE(Differential transcript expression) 和 DTU(Differential transcript usage, DTU)的区别。

>Schematic illustration of differential transcript expression (DTE) and differential transcript usage (DTU) between conditions 1 and 2, for a gene with two isoforms. DTE implies that we can observe expression changes for at least one transcript between condition 1 and condition 2. However, the expression proportion of each transcript (as a percentage of the total expression of all transcripts of the same gene) does not necessarily change between conditions, and thus DTE does not necessarily imply DTU. In DTU, on the other hand, the relative expression of the isoforms of a gene changes between the conditions, whereas the total expression of the gene may or may not remain constant. Since at least one isoform must change expression in DTU, it also implies DTE. The numbers indicated on the transcripts in the figure represent expression levels (in arbitrary units) for easier interpretation. Note that in practice, many genes will have more than two isoforms, but the principal difference between DTE and DTU carries over

嗯，usage定义基本上就是transcript表达量占这个基因所有transcripts总和表达量的比例。

值得注意的有这么几个：
>An early simulation study across a handful of popular mapping-DTU pipelines highlighted that: (i) the presence of DTU can increase false positive rates for standard gene-level differential expression analyses, which is perhaps not surprising, and (ii) in some cases, DTU simply cannot be detected with current methods.

这是文章其中一个引文[13](https://www.ncbi.nlm.nih.gov/pubmed/24365034/ "Blind spots of quantitative RNA-seq: the limits for assessing abundance, differential expression, and isoform switching. Rehrauer H, Opitz L, Tan G, Sieverling L, Schlapbach R, BMC Bioinformatics. 2013 Dec 24; 14():370.")

>They compared performance across different alternative splicing ratios, read depths, dispersion patterns, types of splice changes, and sample sizes, and they explored the influence of annotation, highlighting that no single method dominates in performance and that they often give conflicting results.

[14](https://www.ncbi.nlm.nih.gov/pubmed/25511303/ "Comparisons of computational methods for differential alternative splicing detection using RNA-seq in plant systems. Liu R, Loraine AE, Dickerson JA, BMC Bioinformatics. 2014 Dec 16; 15():364.")


这篇15年的文章更多讨论的是当时几种方法的比较。

---

RNA-seq blog还有[关于DTU的另一篇文章的post](http://www.rna-seqblog.com/gene-level-false-discovery-rate-control-for-transcript-level-analysis-and-complex-rna-seq-experiments/ "Gene-level false discovery rate control for transcript-level analysis and complex RNA-seq experiments")

这和上面那篇有同样的作者， Mark D. Robinson
主要是推荐一种分析流程吧， two-stage testing procedure, stageR
首先在screening阶段，具有有趣的表现的（比如差异表达）的基因先做一个综合测试，比如global F test, global likelihood ratio test, 或者是aggregating p values. 在这个阶段评估的主要是基因水平的FDR。
作用主要是富集那些具有显著作用的基因，并且也可以增加后续DTU背景下分析的power。

然后是confimation阶段，对于每个阶段一筛出来的基因分别测试不同的假设。

结论是具有“dramatic power increase for testing interaction effects and controls the gene-level FDR"

![](http://www.rna-seqblog.com/wp-content/uploads/2017/09/schemePDF.jpg)

[stageR: a general stage-wise method for controlling the gene-level false discovery rate in differential expression and differential transcript usage](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1277-0 "Genome Biology, 2017")


### Footnotes
#### Percent spliced in(PSI) <span id = "PSI"></span>
According to outrigger which is a tool designed for AS calculation:
![](https://yeolab.github.io/outrigger/_static/outrigger_psi-300ppi.png)
