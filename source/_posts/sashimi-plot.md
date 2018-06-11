---
title: How to plot sashimi plot? Tools and their usages
tags:
  - RNA-seq
  - Tools
categories:
  - note
Author: Jason Li
date: 2018-06-11 22:37:53
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

The [paper]((https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4542614/)) for stand-alone sashimi plots was published in 2015.

### Output example
![MISO sashimi_plot](http://miso.readthedocs.io/en/fastmiso/_images/sashimi-plot-example-annotated.png)
Noted that the junction connections were quantified and displayed by junction reads number.

### Shortcomings
Since the inputs require MISO output, it means that
I have to run the whole packages all over. Cannot just plot from bam files.

[update](http://miso-users.mit.narkive.com/KCWQVe7I/sashimi-plot-without-miso):
>Not specifying the miso_files or specifying any directory that does not contain MISO files (or a value like "None") should work.

## [IGV](https://software.broadinstitute.org/software/igv/Sashimi)
### Installation & Dependencies
Download the software [here](https://software.broadinstitute.org/software/igv/download).
Need `igvtools` or [`samtools`](http://www.htslib.org/) to generate index files for each bam.

### Usage & Materials needed
软件可以直接操作看，也可以使用batch script控制
控制命令参考[Controlling IGV through a Port](https://software.broadinstitute.org/software/igv/PortCommands)
但关于sashimi plot的操作似乎还是通过MISO的python 脚本来实现的

[igv-help of google group](https://groups.google.com/forum/#!topic/igv-help/bafUoKYzEVE)
>For scripting I recommend you use the original sashimi plot:  https://miso.readthedocs.io/en/fastmiso/sashimi.html

[igv-documentation for Sashimi plot](https://software.broadinstitute.org/software/igv/Sashimi)
>Static images of Sashimi plots can also be generated outside IGV with sashimi_plot, a Python tool which is part of the [MISO](http://genes.mit.edu/burgelab/miso/) package. Read more about sashimi_plot [here](http://miso.readthedocs.io/en/fastmiso/sashimi.html).

### Output example
![IGV sashimi_plot](https://software.broadinstitute.org/software/igv/sites/cancerinformatics.org.igv/files/SL_Sashimi1.png)

### Shortcomings
不能使用脚本控制
或者还是得调用MISO那一套

## [SplicePlot](http://montgomerylab.stanford.edu/spliceplot/index.html)
### Installation & Dependencies
[GH page](https://github.com/wueric/SplicePlot)

- Python requirements:
    + Python 2.6 or newer . If running Python 2.6, download and install the argparse module
    + numpy version 1.7.1 or newer 
    + scipy version 0.11.0 or newer
    + matplotlib version 1.2.0 or newer
    + pandas version 0.11.0 or newer
    + pysam version 0.7 or newer

- Other requirements:
    + SAMtools must be installed and be in your $PATH
    + Tabix must be installed and be in your $PATH


1. Install the above dependencies.
1. Download the SplicePlot .zip and unpack the archive in the desired directory
1. Check if all of the necessary Python packages are available by running the command python check_module_availability.py in the SplicePlot directory.

Cannot be found on conda cloud.

### Usage & Materials needed
<!-- needs updates of summary -->

Details are shown [here](http://montgomerylab.stanford.edu/spliceplot/index.html#running-spliceplot).

### Output example
![SplicePlot sashimi_plot](http://montgomerylab.stanford.edu/spliceplot/_images/sashimi_sample.png)

Noted that the exon connections are presented as **splicing ratio**, which is calulated as:
![SplicePlot splicing_ratio](http://montgomerylab.stanford.edu/spliceplot/_images/math/453a31526e1d09c7ec4c25bc12199f8824f1facb.png)

And the package can also print out [hive-plots](http://montgomerylab.stanford.edu/spliceplot/index.html#hive-plots) and [Structure-plots](http://montgomerylab.stanford.edu/spliceplot/index.html#structure-plots)

### Shortcomings



>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
