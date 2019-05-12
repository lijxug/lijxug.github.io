---
title: 重装Ubuntu-02
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
重装篇02 
安装Vim和Tmux方便terminal使用
<!--more-->

# Vim
## 安装
```
sudo apt install vim
```

## 配置

- 先装个
    + curl
    + git
    + gawk
    + gcc
```
sudo apt install curl
sudo apt install git
sudo apt install gawk
sudo apt install build-essential
```

- 去github 装个Pathogen
[Pathogen](https://github.com/tpope/vim-pathogen)

- clone 下列包到 ~/.vim/bundle/
    + vim-colors-solarised
    + nerdtree
    + indentLine
    + vim-airline
    + auto-pairs

拷入老机子上的.vimrc以后测试运行，完美收工

# tmux

## 安装

```
# 安装依赖
# libevent 2.x
wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
tar xvf libevent-2.1.8-stable.tar.gz
cd libevent-2.1.8-stable
./configure
make
sudo make install

# ncurses
wget https://invisible-mirror.net/archives/ncurses/ncurses-6.1.tar.gz
tar xvf ncurses-6.1.tar.gz
cd nurses-6.1
./configure
make
sudo make install

# 安装本体
git clone https://github.com/tmux/tmux.git
cd tmux

# 从这里需要装automake
sudo apt-get install automake
sudo apt-get install pku-config

sudo sh autogen.sh
./configure 
make && sudo make install
```

安装以下插件
- tpm
- tmux-sensible
- tmux-resurrect

大功告成






>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
