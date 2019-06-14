---
title: 重装Ubuntu-04 工作环境
tags:
  - Linux
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
重装篇04 
- R/Rstudio-server
- jupyter lab server style
<!--more-->

# 脚本开机启动

构造开机脚本`startup.sh`
并且确保开头具有
```
#!/bin/bash
PATH=$PATH:/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/bin
SHELL=/bin/bash

/path/to/SendIP.sh
/path/to/check_ss.sh
```

之后使用crontab设置开机启动
```
sudo crontab -e
# 在脚本后加入
@reboot /path/to/startup.sh
```


# 美化
MacOs 主题
[教程](https://www.jianshu.com/p/6ef16e3b0a3e)

桌面幻灯片
Variety



>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
