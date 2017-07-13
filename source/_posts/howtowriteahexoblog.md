---
title: 如何写Hexo博客
tags:
  - hexo
  - markdown
categories:
  - memo
date: 2017-05-13 00:38:35
---
### 前言
这是一篇备忘，用来记录Hexo博客从新建到完成的过程和其中涉及到的细节。

<!-- more -->

### 新建页面
在bash里输入以下代码，就可以看到在博客目录`/_posts`下出现你想要的页面了。
```bash
hexo new [layout] <title>

### example
hexo new "test"
```

### 编辑header
在`\_posts`下找到刚新建出来的文件，使用你喜爱的文本编辑器打开
大概长这样,被`---`框在中间
```
---
title: 'test'
date: 2017-05-13 13:27:14
---
```
可以加入tags和categories
```
---
title: 'test'
date: 2017-05-13 13:27:14
tags:
  - hexo
  - markdown
categories:
  - memo
---
```
如果你有评论区，可以把它关掉
```
---
title: ''
date: 2017-05-13 13:27:14
tags:
  - hexo
  - markdown
categories:
  - memo
comments: false
---
```

### 编辑内容
Hexo支持的博文使用[markdown](http://wowubuntu.com/markdown/ "Markdown语法说明")语法，这里就不再赘述，仅贴出一些特殊格式的代码示例。

### 列表
**输入**
```
 # 无序列表
- ha
- yo
 # 有序列表
1. yo
2. he
```

**展示效果**
- ha
- yo

1. yo
2. he

### 引用
```
> Hello, world!
```

>Hello, world!

### 链接
**行内式**:比如上面链接的那个[markdown](http://wowubuntu.com/markdown/"Markdown语法说明")
```
[markdown](http://wowubuntu.com/markdown/ "Markdown语法说明")
```

**参考式**：还是拿[markdown][1]举例吧。
[1]: http://wowubuntu.com/markdown/ "Markdown语法说明"
```
参考式：还是拿[markdown][1]举例吧。
[1]: http://wowubuntu.com/markdown/ "Markdown语法说明"  # 可以放在文章任意地方
```
或**隐式参考**: 就像这样[markdown][]
[markdown]: http://wowubuntu.com/markdown/ "Markdown语法说明"
```
或**隐式参考**: 就像这样[markdown][]
[markdown]: http://wowubuntu.com/markdown/ "Markdown语法说明"  # 同上

```

### 图片
一些图片![my figure](/imgs/avatar.jpg "我的头像")
```
一些图片![my figure](/imgs/avatar.jpg "我的头像")
```

同样也有*参考式*：![my figure][1]
[1]: /imgs/avatar.jpg "我的头像"
```
同样也有*参考式*：![my figure][1]
[1]: /imgs/avatar.jpg "我的头像" # 同样也可以放在文章任意位置, 当然，推荐放最后
```

### Hexo的资源组织方式[asset_folder](https://hexo.io/zh-cn/docs/asset-folders.html)
使用`asset_folder`可以更加直观清晰地对文件进行管理。

{% asset_img avatar.jpg This is an example image %}

```
{% asset_img avatar.jpg This is an example image %}
```

### Tips
1. `<!-- more -->`：`阅读全文`功能
2. 特殊引用
{% cq %} What doesn't kill you makes you stronger. {% endcq %}
```
{% cq %} What doesn't kill you makes you stronger. {% endcq %}
```

### 最后
得感谢一下z尼玛大力安利和技术支持:
[z尼玛的博客](https://kevinzjy.github.io/)

>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！