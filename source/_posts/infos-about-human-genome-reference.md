---
title: 'Some Information about Human Genome Assembly & Annotation '
tags:
  - genome
categories:
  - note
Author: Jason Li
date: 2018-06-26 16:27:35
---


<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  TeX: { equationNumbers: { autoNumber: "AMS" } }
});
</script>

# Abstract
Recently, I found some strange expressed transcripts in my results, **PTPRC-220**, for example . After searching for details, it turned out to be a transcripts annotated to be locate on a contig named **"GL383520.2"** .


<!--more-->

# What are those region with strange names

In [GENCODE](https://www.gencodegenes.org/) database, the curated Genome sequence file contain some strange "region" with names started with "GL" or "KI", etc. 

Besides, some of the these regions contained fragments with names like "HSCHR6_MHC", according to [this letter](http://seqanswers.com/forums/archive/index.php/t-4459.html), which suggests that 

>All the files with "HSCHR" in the file name are haplotype variants, e.g., the "HSCHR6_MHC" files contain variants to the the MHC region of chromosome 6. I suggest to simply not include these files when building the reference (unless, of course, you are specifically interested in them, but then you need to do some additional tweaking).

These region, according to [this question on biostars](https://www.biostars.org/p/215787/)

>`GL000008.2` is a contig from somewhere on chromosome 4. There are a large number of these. 
`KI270330.1` is an unplaced scaffold that is presumed to belong to the human genome.

# Which chromosomes/scaffolds/patches to include?
According to [STAR manual](http://labshare.cshl.edu/shares/gingeraslab/www-data/dobin/STAR/STAR.posix/doc/STARmanual.pdf), it recommands that,
>to include major chromosomes (e.g., for human chr1-22,chrX,chrY,chrM,)
as well as un-placed and un-localized scaffolds. 

...

>a substantial number of reads may map to ribosomal RNA (rRNA) repeats on these scaffolds. These reads would be reported as unmapped if the scaffolds
are not included in the genome, or, even worse, may be aligned to wrong loci on the chromosomes.
Generally, patches and alternative haplotypes should **not** be included in the genome.

# Conclusion

Seems that there is different thoughts about whether to include un-placed & un-localized scaffolds ...


>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
