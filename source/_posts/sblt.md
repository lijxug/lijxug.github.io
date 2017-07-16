---
title: Sublime Text3 安装与配置
date: 2017-05-13 21:57:34
tags: [Sublime Text 3, vim, config]
categories: memo
---
### 前言
因为windows的bash装的vim有一点问题，懒得调整了，所以改用了sublime text3（对，因为听说可以用vim mode，我是vim成瘾患者_(:зゝ∠)_）。并且，趁此机会刚好可以用它来写心仪已久的markdown文本，也许再学点别的比如LaTeX。

<!-- more -->

### 下载&安装
前往[Sublime Text官网](https://www.sublimetext.com/3)下载你喜爱的版本。下载成功以后找一个你喜欢的地方装上。细节略去不表。
### 安装拓展包
最先安装的是[package control](https://packagecontrol.io/installation "Package control安装官方教程")。 我装的时候直接用**Manual**方式进行安装，一键搞定，还是很方便的。`package control`顾名思义，就是一个用来方便管理包的扩展包。功能上类似python的`pip`。 在sublime text里使用可以直接以一种近似图形界面的方式使用。

如图所示，`ctrl+shift+P`调出command窗口，点开以后可以在package列表中搜索你想要的package，一键安装。 

{% asset_img inst.jpg origin %}

下面安利几个包。

* 对于资深vim用户: 想要开启vim mode，有两个选择。

    1.在`Preferences -> settings`里将`"ignored_packages`字段设为空。即使用sublime text3自带的*Vintages*包，这个包支持vim ctrl keys。如果你想用它，那就在`settings`里做如下修改
    ```
    "ignored_packages": [ ],
    "vintage_ctrl_keys": true
    ```
    可惜的是这个包不支持vim的命令行命令，目前只支持`:w`和`:e`。

    2.或者你可以使用一个叫做[vintageous](https://github.com/guillermooo/Vintageous)的包。这个包可以使用包括查找和替换在内的大多数vim的cmd命令，使用package control可以很方便地安装它。不过需要禁用原生的Vintage包。开启ctrl key方法类似。
    ```
    "ignored_packages":
    [
        "Vintage"
    ],
    "vintageous_use_ctrl_keys": true
    ```

* 其他

|    包名            |        功能         |   适用人群  |
|:----------------:|-------------------|:-------:|
|ConverToUTF8      |自动将不支持的编码方式转成UTF-8 | 非英文用户   |
|Anaconda          |代码补全等              |python用户|
|BracketHighlighter|显示配对括号             |all users|
|OmniMarkupPreview  |预览markdown         |MD用户     |
|MarkdownEditing   |帮助编辑MD文档           |MD用户     |
|SideBarEnhancements   |增强侧边栏功能,复制删除重命名等           |MD用户     |
|To be explored    |        ...        |  ...    |

\* SideBar 可在`View -> Side Bar` 下调出
\* OmniMarkupPreview可以通过快捷键`ctrl + alt + O`实时预览markdown效果，十分好用，但在我电脑上出现了404问题。具体解决办法是在`Preferences -> Package Settings -> OmniMarkupPreview -> Settings - User`下输入

```
{
    "renderer_options-MarkdownRenderer": {
        "extensions": ["tables", "fenced_code", "codehilite"]
    }
}
```

### 键位设置
由于我选择了vim mode，有一些原本sublime text预设的比较好用的键位就会和vim键起冲突。不过好在`alt`键还有很多富裕，所以就设置了一些键位到`alt`键上。
另外，vim里的`ctrl+c`我用的不多，但在windows里这可是一个很常用的键位，所以还是手动改成windows的键位。记录在此，仅供参考。
```
[
    {"keys": ["alt+m"], "command": "markdown_preview", "args": { "target": "browser"}},
    {"keys": ["alt+]"], "command": "indent"},
    {"keys": ["alt+["], "command": "unindent"},
    { "keys": ["ctrl+c"], "command": "copy" },
]
```

最后，附上我的`Settings`作为参考：
```
{
    "color_scheme": "Packages/Color Scheme - Default/Solarized (Dark).tmTheme",
    "enable_highlight": true,
    "font_face": "Consolas",
    "font_size": 14,
    "ignored_packages":
    [
        "Vintage"
    ],
    "vintageous_use_ctrl_keys": true
}
```
>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！