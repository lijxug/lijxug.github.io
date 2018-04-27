---
title: For Fun: Analyse the Height requests distribution
tags:
  - scrapy
  - forfun
categories:
  - memo
author: Jason Li
---
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Abstract

I noticed that most girls seems to prefer a tall guy (eg. > 170) on the PKU bbs,
  thus the short ones (like me... sad face) could easily end up alone? LOL.

Anyway, I cannot draw any conclusion until I have the data.
So, let's play.

<!--more-->

# Setup analyse environment

I planned to use python3 tools like `scrapy` and `beautifulsoup` to acquire "clean data" from the website,
and use `pandas` to organize data and `` for words frequencies(?)

Since the packages dependencies could be too much works, I prefer to start over with a brand new environment using Anaconda.

```
conda create -n web_data_analyse python=3.6
source acitvate web_data_analyse
conda install -c conda-forge scrapy
conda install -c conda-forge beautifulsoup4

```

# Use scrapy spider to get websites


# Use BeautifulSoup4 to parse these websites and get the main content of them

# Construct word frequencies data matrix

# Plots & Conclusions















>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
