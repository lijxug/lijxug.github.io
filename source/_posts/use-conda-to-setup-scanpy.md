---
title: Use conda to install scanpy
tags:
  - python
  - conda
  - single-cell
categories:
  - memo
author: Jason Li
date: 2018-03-24 14:09:44
---


### Preface

最近*Genome Biology*发了一个基于python的单细胞分析工具，针对目前越来越大的单细胞数据进行了优化，速度很快。
所以尝试用conda安装看看，方便管理环境。

文章链接：[SCANPY: large-scale single-cell gene expression data analysis](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1382-0)

Github: [Scanpy – Single-Cell Analysis in Python](https://github.com/theislab/scanpy)

<!--more-->

### Procedure

本机系统
```{shell}
sudo lsb_release -a
#> No LSB modules are available.
#> Distributor ID: Ubuntu
#> Description:    Ubuntu 16.04.4 LTS
#> Release:        16.04
#> Codename:       xenial
```

设置一下镜像站
```{shell}
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

创造环境
```{shell}
conda create -n scanpy python=3.6
```

国内镜像应该很快，等待安装完成。。。

激活环境，安装scanpy及其依赖，根据[文档](https://scanpy.readthedocs.io/en/latest/installation.html)，依赖顺序很重要

```{shell}
source activate scanpy
pip install scanpy
```

Oops，报错了

{% asset_img p1.png %}

更新一下pip重新再装一次
```{shell}
pip install --upgrade pip
```

仔细看了一下。。好像是网速的问题。。

通过国内镜像安装
```{shell}
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple scanpy
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple python-igraph
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple louvain

```

完成。没出什么问题。




