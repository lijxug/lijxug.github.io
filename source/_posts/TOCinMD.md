---
title: TOC in MD
date: 2017-07-07 16:27:41
tags:
    - markdown
categories:
    - memo
---

# Introduction
I am working on a README file for a project recently. These files are commonly written by MarkDown. However, I can't help noticing that some documentations contain hyperlinks which act as index. So I tried to figure out how to add **TOC**(**T**able **O**f **C**ontents) in a Markdown file.

<!-- more -->

# Method
## Add TOC manually
Use tags like `<h1 id = "1">foo</h1>` and `[foo](#1)` to make hyperlinks. For example:

For better understanding, I'd like to drop an anchor here. :P

- [foo](#foo)
    * [foo1](#foo1)
    * [foo2](#foo2)

The code for the upper TOC is like:
```
For better understanding, I'd like to drop an anchor here. :P

- [foo](#foo)
    * [foo1](#foo1)
    * [foo2](#foo2)

```


And the code for the header is sth like:
```
For better understanding, I'd like to drop *another* anchor here. :P
<h4 id = "foo">foo</h4>
jibber-jabber
<h5 id = "foo1">foo1</h5>
jibber-jabber
<h5 id = "foo2">foo2</h5>
jibber-jabber
```

For better understanding, I'd like to drop *another* anchor here. :P
<h4 id = "foo">foo</h4>
jibber-jabber
<h5 id = "foo1">foo1</h5>
jibber-jabber
<h5 id = "foo2">foo2</h5>
jibber-jabber


Then you understand how this works.

It's a robust way to add TOC.

## Add TOC automatically

Well, as far as I know, There is not a general way at present. Some claim that add `[TOC]` at the position you want would do the trick. Let me try it here...

[TOC]

Well, nothing happens. I guess this function depends on the compiler or the editor. 

One the other hand, in RMarkDown, one can add TOC by using the following lines in the header. 
```
---
title:
output: 
    html_document:
    toc: true
    toc_float: true
---
```

>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！