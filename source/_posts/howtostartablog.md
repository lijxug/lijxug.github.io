---
title: Windows下使用HEXO + Github建立个人博客
date: 2017-05-13 16:04:21
tags: [hexo, github, NexT]
categories: memo
---
# 前言
在Kevinzjy的怂恿下开了这个blog，打算用来记录一下平时的一些小技巧。那么自然，先从怎么开启这个blog开始记录好了。

<!-- more -->

# 安装Git & Node.js
从[git官方网站](https://git-scm.com/)下载适合自己操作系统的git安装包，打开安装。
然后下载[Node.js](https://nodejs.org/en/)安装包进行安装。

# 安装[Hexo](https://hexo.io/zh-cn/docs/)
打开bash，或者git bash，利用以下命令安装hexo
```
npm install hexo-cli -g
```

# hexo初始化
找一个喜欢的文件夹作为blog根目录，在路径下打开bash，运行
```
hexo init
npm install
npm install hexo-deployer-git --save # 安装git插件
hexo clean
hexo g # == hexo generate 生成静态文件
hexo d # == hexo deploy 部署到远端（如github)

hexo s # == hexo server 启动本地web服务，用于预览
```

现在打开[http://localhost:4000/](http://localhost:4000)应该就可以看到一个页面了。这就是你的blog在本地时候的样子。接下来我们要把它部署到网上。


# 获取[github page](https://pages.github.com/)
前往[github](https://github.com), 登录账号。
点击`new repository`新建一个远程仓库,仓库名字必须是**username/username.github.io**
然后将clone or download下形如`https://github.com/your-username/your-username.github.io.git`的git路径复制下来
填入hexo根目录下的*_config.yml*中`deploy`字段，如下所示：
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/your-username/your-username.github.io.git
  brach: master
```
然后再次运行
```
hexo g
hexo d
```
即可

# 修改hexo主题
推荐使用主题[NexT](http://theme-next.iissnan.com/)，集简洁和优雅于一体，而且使用方便。
在bash下，切换到你之前选定的根目录文件夹，运行如下所示命令
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
完成后，打开刚刚那个**_config.yml**文件，找到`theme`字段，将值改为`next`
```
theme: next
```
之后重新产生静态页面并部署，就能看到主题改变。
其他主题还有很多，如果想试试别的主题可以参考[hexo themes list](https://github.com/hexojs/hexo/wiki/Themes)

# 其他
## 设置背景图片
下载喜欢的图片，放到*主题*目录`/source/images/`
打开`/theme/next/source/css/_custom/custom.styl`,添加如下代码
```
body{
    background:url(/images/your-photo.jpg);
    background-attachment: fixed;    # 背景图片不跟随屏幕滚动
}
```

## 设置背景透明度
**文章背景**
打开`/theme/next/source/css/_schemes/Pisces/_layout.styl`,将`.content-wrap`下的`background`字段改成：
```
  background: rgba(255,255,255, 0.6); # 0.6即为透明度
```

**按钮背景**
打开`themes\next\source\css\_common\components\post\post-button.styl`
将`.btn`下`background`字段改为:
```
    background: transparent;
```

**侧边栏背景**（感谢[Acris Liu](https://github.com/Acris)的帮助）
之前一直没能找到直接修改侧边栏透明度的方法，在Acris的帮助下找到了。
在`themes\next\source\css\_common\components\sidebar\sidebar.styl`中`.sidebar`下
```
    opacity: 0.6
```

**菜单栏背景**
`themes\next\source\css\_schemes\Pisces\_layout.styl`
```
.header_inner{
    background: rgba(255,255,255, 0.6);
}
```

>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！