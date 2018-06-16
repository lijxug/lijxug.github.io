---
title: 'dplyr: mutate new column based on multiple selected columns'
tags:
  - R
  - dplyr
categories:
  - tip
Author: Jason Li
date: 2018-06-16 10:29:26
---


<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Abstract

As title shown, a trick for manipulating data frame.

<!--more-->

# Main

The original question is shown [here](https://stackoverflow.com/questions/42332005/dplyr-mutate-new-column-based-on-multiple-columns-selected-by-variable-string)

The best answer was
```{R}
mycols <- '(x2,x5)'
f <- paste0('min',mycols)
df %>% rowwise() %>% mutate_(min = f)
df
# A tibble: 10 × 6
#      x1    x2    x3    x4    x5   min
#   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#1      2     3     0     1     1     1
#2      0     2     1     0     1     1
#3      0    NA     0    NA    NA    NA
#4     NA     5     1     3     1     1
#5      0     3     3     0     3     3
#6      1     2     0     0     4     2
#7      1    NA    NA    NA    NA    NA
#8     NA    NA    NA     0     3    NA
#9      0     4     0     0     3     3
#10     1     5     1     1     1     1
```











>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
