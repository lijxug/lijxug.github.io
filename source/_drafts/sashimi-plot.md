---
title: How to plot sashimi plot? Tools and their usages
tags:
  - RNA-seq
  - Tools
categories:
  - notes
Author: Jason Li
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Abstract
总结一下sashimi plot相关的方法，找一个最适合我现在状况的方法。

<!--more-->
# What is sashimi_plot?
>Sashimi plots first appeared as a part of the MISO package developed by Katz et. al. in 2010. They allow for the easy comparison of read depth, alternative splicing, and isoform structure between individual RNA-seq samples.

This introduction comes from [SplicePlot](http://montgomerylab.stanford.edu/spliceplot/index.html)

# 现存的几种方案
## [MISO](http://miso.readthedocs.io/en/fastmiso/sashimi.html)

### Installation & Dependencies
[MISO whole package](http://genes.mit.edu/burgelab/miso/software.html)

`sashimi_plot` itself only requires Python package matplotlib(version 1.1.0 or higher) as well as samtools

### Usage & Materials needed

- GFF file recording the informations of your alternative events
- setting.txt
    + bam_files
    + miso_files
    + plot settings
    + Bayes factors thresholds for --plot-bf-dist

Inputs require a gff file of the alternative events, which has to be **indexed** in order to be used with MISO with the `index_gff` script.

plot a event by running following command line from within the `sashimi_plot` directory in MISO:
```
sashimi_plot --plot-event "chr17:45816186:45816265:-@chr17:45815912:45815950:-@chr17:45814875:45814965:-" test-data/event-data/ settings/sashimi_plot_settings.txt --output-dir test-plot
```

the event name is listed in the GFF file

### Output example
![MISO sashimi_plot](http://miso.readthedocs.io/en/fastmiso/_images/sashimi-plot-example-annotated.png)

### Shortcomings
Since the inputs require MISO output, it means that
I have to run the whole packages all over. Cannot just plot from bam files.

## [IGV](https://software.broadinstitute.org/software/igv/Sashimi)
### Installation & Dependencies
### Usage & Materials needed
### Output example
### Shortcomings

## SplicePlot
### Installation & Dependencies
### Usage & Materials needed
### Output example
### Shortcomings











>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
