---
title: Comparation of STAR-based/kallisto pipeline
tags:
  - STAR
  - kallisto
  - RNA-Seq
categories:
  - refs
Author: Jason Li
date: 2018-04-27 11:43:31
---


# Preface
Actually this post works as a link to [one of **crazyhottommy**‘s posts](https://github.com/crazyhottommy/RNA-seq-analysis/blob/master/salmon_kalliso_STAR_compare.md) which answered a lot of questions of transcripts quantificaiton that have haunted me for a long time.

<!--more-->

# What I've learned in this post

## Details of definition of effective length which should be used while calculating TPMs

Check the post for more details.

Also it provide the scripts to acquire effective length which is really helpful.

Well, I think it's quite straightforward I think...


## General idea of differences between alignment-based & alignment-free method

![Counts correlation between two align-free method](https://cloud.githubusercontent.com/assets/4106146/16748683/2717a796-478b-11e6-9744-4e477f2a3c15.png)

![Correlation between STAR derived counts and kallisto derived est_counts](https://cloud.githubusercontent.com/assets/4106146/16748683/2717a796-478b-11e6-9744-4e477f2a3c15.png)

## alignment-free method comparation

Acoording to [another post](https://sjcockell.me/2015/05/18/alignment-free-transcriptome-quantification/) which focus on the comparation between alignment-free methods, ...

Salmon and kallisto both did a pretty great job.

![kallisto vs 'truth'](https://sjcockell.files.wordpress.com/2015/05/kallisto_truth.png)

![non-bias Salmon counts vs 'truth'](https://sjcockell.files.wordpress.com/2015/05/nbc_salmon_truth.png?w=940&h=635)

![comparation between TPM derived from two method](https://sjcockell.files.wordpress.com/2015/05/nbc_tpm_compare.png)

The conclusions from two posts are similar. Still, it seems that the est_counts from kallisto is slightly better than Salmon non-bias corrected counts.


>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！