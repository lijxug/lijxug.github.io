---
title: 'For Fun: Analyse the Height requests distribution'
tags:
  - scrapy
  - forfun
categories:
  - memo
author: Jason Li
date: 2018-04-29 09:15:13
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

I planned to use python3 tools like `scrapy` to acquire "clean data" from the website,
and use `pandas` to organize data and `jieba` for Chinese text segmentation.
Finally, I'd like to use `R::tidyverse` to plot :P .

Since the packages dependencies could be too much works, I prefer to start over with a brand new environment using Anaconda.

```
conda create -n web_data_analyse python=3.6
source acitvate web_data_analyse
conda install -c conda-forge scrapy

```

# Use scrapy spider to get websites

The tutorial for scrapy spiders are shown [here](https://doc.scrapy.org/en/latest/intro/tutorial.html#intro-tutorial).

after a pretty long time struggling in these documentations, ... I've got a spider!

`spider.py` 

```{python}
# -*- encoding: utf-8 -*-
import scrapy
from bbs.items import PostItem

class bbsSearchSpider(scrapy.Spider):
    name = "bbs_heights"

    start_urls = [
        'https://bbs.pku.edu.cn/v2/search.php?mode=post&bid=167&key=for+gg&days=7'
    ]

    def parse(self, response):
        
        for block in response.css('div.block'):
            # found Re in the second span means the original post was removed, it is quite possible that extraction for height requests ends up in failure.
            if block.css("span::text")[1].extract().find("Re") == -1: 
                post_url = block.css("a.block-link::attr(href)")[0].extract()
                
                # construct postItem
                post = PostItem()
                post['post_id'] = block.css("span.from::text").extract()
                post['publish_time'] = block.css("span::text").extract()[-1]
                post['post_url'] = post_url
                # follow post links while passing postItem to the postparser
                yield response.follow(post_url, meta = {'item': post}, callback=self.parse_post)
            
        # follow pagination links
        button_text = response.css('div.paging-button::text').extract()
        next_page = response.css('div.paging-button a::attr(href)')[button_text.index('下一页 >')].extract() 
        if next_page is not None:
            # next_page = response.urljoin(next_page)
            yield response.follow(next_page, callback=self.parse)
        
    def parse_post(self, response):
        # extract postItem from the last callback
        item = response.meta['item']
        # extract content of each post
        main_body = response.css("div.body")[0]  # first floor
        main_string = "".join(main_body.css("p::text").extract())
        main_string = "".join(main_string.split())  # rejoin to remove \xa0
        item['content'] = main_string
        yield item

```

While `PostItem` class was defined in `item.py`
```{Python}
# -*- coding: utf-8 -*-

# Define here the models for your scraped items
#
# See documentation in:
# https://doc.scrapy.org/en/latest/topics/items.html

import scrapy

class PostItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    post_id = scrapy.Field()
    publish_time = scrapy.Field()
    post_url = scrapy.Field()
    content = scrapy.Field()
```

After running the command line tool
```
scrapy crawl bbs_heights -o bbs.jl
```

I've acquired all the posts contents I want within 7 days on the BBS!

Since the data was exported in `jsonline` format, I have to install an additional packages for easily reading jsonlines.
```
pip install jsonlines
```

# Parse contents to height requests data
## Data cleaning
The data we scraped is well-organized yet not suitable enough for downstream analysis.

So, I tried some ways to do the data laundry and make sense of it.

## Parse contents to words

Download jieba for Chinese text segmentation 
```
pip install jieba
```

After remove the stopwords, the remained words seemed prettier. However, I was hoping that text segmentation would help me to get some key information to understand **the context of each height data**. The fact is, it cannot. Or I just haven't get the main idea of analysing linguistic data. 

## Extract height data

Use `re`, of course.

However, it's trickier than I expected. For some of the heights text are pretty strange and funny, like `165cm60kg` or `一七六`. I choose to neglect the Chinese character version of heights and focus on extract serveral funny forms of numeric heights. 

Well... in the end I've come up with a solution, it's not elegant I have to admit, but it works (for now).

The function are shown below.

```
# value words detection
def value_words_detection(lst):
    # split_words = ['要求', '希望', '期待']  
    # split_pattrn = re.compile(r'|'.join(split_words))
    height_pattrn = re.compile(r'1[5-9]\dc?m?') # have to check whether followed by '.com'
    com_pattrn = re.compile(r'com') # have to check whether followed by '.com'
    
    # found all patterns above in words list
    found_word = list()
    for idx, word in enumerate(lst):
        # match_split = re.match(split_pattrn, word)
        # if match_split:
        #     found_word.append(word)
        
        match_split = re.match(height_pattrn, word)
        if match_split: 
            if (idx + 1) >= len(lst):
                continue
            if lst[idx+1] == "com":
                continue
            height = float(word.split('cm')[0])  # ugly way to extract height...
            if height < 200 :
                found_word.append(height)  
    
    return(found_word)

```

You can see some "trying efforts" in it... 

# Plots & Conclusions

Well, cut to the chase.

I've plot the post counts along the publish data and the mentioned heights distribution trying to get a general idea of the data set.

{% asset_img fig1.png fig1 %}

{% asset_img fig2.png fig2 %}

And the key point, which is **whether the girls prefer guys who are over 170 cm**, was demonstrated pretty clear in fig3&fig4, I think. 

{% asset_img fig3.png fig3 %}

{% asset_img fig4.png fig4 %}


Basic analysis were writen in [my post](https://bbs.pku.edu.cn/v2/post-read.php?bid=167&threadid=16400805) on PKUBBS.

I am NOT going to repeat here, too much trouble...


>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！