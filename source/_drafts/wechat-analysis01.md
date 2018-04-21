---
title: 玩耍:微信聊天数据分析 01
tags:
  - wechat
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

趁着刚讲完组会，在周末研究一下分析自己的微信聊天数据。
大致可能会有这么几步，

- 导出数据，解码，整理出词频/聊天对象表
- 对总体进行基本统计作为QC，可能包括总体聊天条目，样本词频分布，去掉一些无义词频和低交流度的对象，句式复杂度分布(不知道有没有意义)
- 针对关键词的分析，包括词云，关键词（如哈哈哈）的基本统计
- 针对样本（即聊天对象）的分析
- 尝试进行聚类和可视化，看看是不是可以按照聊天态度分群233

第一部分，做到哪算哪。也算磨炼一下自己的数据分析技巧吧233
<!--more-->

# 导出数据
我用的手机是MI6，使用的电脑是miniMac
[这篇知乎](https://www.zhihu.com/question/19924224)的做法gg，第一步插电脑就毫无反应

尝试参考[这篇知乎](https://www.zhihu.com/question/24488996)的做法先试试。
直接通过微信电脑版备份聊天记录到电脑，然后再看看是不是可以破解备份文件。

查找到电脑上的备份存放文件夹是`~/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/`，进去以后发现多了一个几G的文件夹，数据应该就在这了

Backup最大，看看里面都有啥
发现里面是个`.db`数据库。

根据[这篇文章](https://www.2cto.com/article/201507/414509.html)
猜测这个数据库是以同样的方式加密的。
即 
```{python}
KEY = MD5( IMEI + UIN )[ 0:7 ]
```

IMEI通过在手机拨号屏幕输入`*#06#`即可获得
UIN通过[这篇文章](https://jingyan.baidu.com/article/e3c78d644a59f33c4c85f530.html)描述的方法可以得到，不过我得到的是10位数字。
尝试计算得到key

因为我用的是mac，所以直接在terminal用MD5命令就行了
```
md5 -s "IMEI-UIN"`
```

取前7位作为key
用命令行工具sqlcipher打开Backup.db，输入`PRAGMA key = 'yourkey'; `
得到提示file is not a database

莫不是解密失败。。gg

找了一圈发现网上大多数都是root权限然后获取EnMicroMsg.db
然而我的小米6是MIUI9稳定版，获得root权限颇为艰难，而且要清空储存..gg










>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！