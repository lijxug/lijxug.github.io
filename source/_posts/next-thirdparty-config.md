---
title: NexT的第三方功能配置
date: 2017-05-16 23:03:44
tags: NexT
categories: memo
---

### 前言
在搭博客的时候配置好主题是一回事，围绕主题搭好第三方支持又是另一回事。所幸，NexT十分优秀，里面集成了很多第三方功能，有些时候只需要配置一下即可使用，省去了我们不少插入html代码的麻烦。

<!-- more -->

大家重点参考[NexT官网第三方服务集成文档](http://theme-next.iissnan.com/third-party-services.html)，我在这记录的是我用过的觉得好用的，只能作为经验，并不全面，也不一定客观正确。不过为了让自己能记得哪些服务比较重要，还是在这记录一下。
我的NexT版本是`5.1.1`，不同的版本配置文件可能会有些许不同。

NexT的第三方服务配置可以在`主题配置文件`, 也就是`themes/next/_config.yml`文件，搜索
```
# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------
```

### 评论系统

考虑到国情和网速问题，我首先想支持的还是国货。
#### [网易云跟帖](https://gentie.163.com/)
但是这是个扶不起来的阿斗，在注册站长填资料的时候它不认`*.github.io`域名，总觉得这是个别人注册过的域名，gg。

所以在朋友**Kevinzjy**的建议下，虽然看不懂韩文，我还是向现实低头，用了来必力。
#### [来必力](https://livere.com/)
说句公道话，来必力做的还是不错的，支持简体中文，注册也方便。除了偶尔蹦出来的韩语外，没有太大毛病。注册之后点网页上方导航栏的安装。
{% asset_img livere01.png %}

然后选那个免费的。

{% asset_img livere02.png %}
{% asset_img livere03.png %}

找到**代码管理**以后把上面**涂黑**的那一段你自己的身份识别代码复制出来，填到`livere_uid`字段后就行了，记得把注释去掉。

```
# Support for LiveRe comments system.
# You can get your uid from https://livere.com/insight/myCode (General web site)
# livere_uid: XXXXXXXXXXXXXXXXXXXX
```

大功告成。之后你在载入博文的时候，只要没有在头部定义`comments: false`，就会出现评论区了。

### 网站流量数据分析

作为一个伪程序员，我也迷信Google。不得不说百度比起Google还有很多发展空间，虽然没什么流量到我的博客（哈哈哈_(:зゝ∠)_）。

#### [Google Analytics](https://www.google.com/analytics/)
实用性和易用性我就不吹嘘了，总之这个面向大企业的应用能面向我这种个人用户免费开放我就很开心了。注册登录以后，在管理页面里可以看到一个跟踪ID，一般以**UA**开头。
{% asset_img analytics01.png %}

复制黏贴，填到`_config.yml`里的`google_analytics`字段下即可。
```
# Google Analytics
google_analytics: UA-XXXXXXXXXX
```

#### [不蒜子统计](http://ibruce.info/2015/04/04/busuanzi/)
之所以再加这个是为了网页最下面那个小人和眼睛。_(:зゝ∠)_我觉得十分讨喜。
这个配置比较容易，详情如下。当然，`*_header & *_footer`也可以什么都不写，走简约风格。
```
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true # 开启

  # custom uv span for the whole site
  # 效果：本站访客数12345人次
  site_uv: true
  site_uv_header: 本站访客数
  site_uv_footer: 人次

  # custom pv span for the whole site
  # 效果：本站总访问量12345次
  site_pv: true
  site_pv_header: 本站总访问量
  site_pv_footer: 次

  # custom pv span for one page only
  # 效果：本文总阅读量12345次
  page_pv: true
  page_pv_header: 本文总阅读量
  page_pv_footer: 次
```

### 站内搜索
我用的**Local search**，细节懒得写了，偷偷摘抄一下[官方文档](http://theme-next.iissnan.com/third-party-services.html)~
{% asset_img local.png %}

### 其他

#### [MathJax](http://mathjax-chinese-doc.readthedocs.io/en/latest/start.html "MathJax Chinese Doc 2.0")
```
# MathJax Support
mathjax:
  enable: true
  per_page: false
  cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
```
这个工具主要比较适合需要输入数学公式的朋友。将`enable`字段改成`true`应该就可以使用。我目前用到比较少，所以不敢瞎说，具体使用方法可以参考上面的超链接。

### To be continued ..
建站不久，暂时还没有集成太多功能。看到其他人的博客有**赞赏**啊**分享**啊啥的还是比较眼馋的。有时间慢慢更新吧~


>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！