---
title: 重装Ubuntu-01
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
重装篇01 
分盘，安装及基本系统设定

<!--more-->

# 系统重装版本
Ubuntu 18.04.2 LTS

# 重装步骤

## 启动盘
根据[教程](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0) 使用rufus 创建Ubuntu启动盘
- 选择下载好的ubuntu-18.04.2-desktop-amd64.iso镜像文件
- 按照ISO Image mode写入

泡杯茶等它完成
## 重装

- 插入U盘，重启待安装电脑
- F12选择安装盘启动
- 重新分盘，参考[blog](https://blog.csdn.net/u012052268/article/details/77145427/) 
我有120G和240G两块SSD和32G内存为例，
EFI分区 0.5G
内核/boot预留0.5G
因为我使用中常常要用到大量内存，所以留出32G作为swap空间
剩下都是/
128G SSD都是/Home

试试看
按照顺序

|分区类型|分区容量（MB）|分区位置|文件系统|挂载点|
|---|---|---|---|---|
|Primary|500|Beginning|EFI|-|
|Primary|500|Beginning|Ext4|/boot|
|Primary|32000|Beginning|Swap|-|
|Primary|-|Beginning|Ext4|/|
|-|Another SSD|-|Ext4|/home|

- Install Now!
- 泡个茶等待一下

大功告成

就有鬼了

## 机械数据盘不识别问题

###格式支持

初步猜测是因为不支持ntfs，顺便把exfat也装一下

安装ntfs支持
```
sudo apt-get isntall ntfs-3g
```

安装exfat支持
```
sudo apt-get install exfat-fuse exfat-utils
```

###开机挂载

```
sudo blkid #获取UUID和分区类型
sudo mkdir /media/data #创建挂载点
sudo vi /etc/fstab #使用vi编辑挂载配置文件
#填入以下，并全部用空格隔开
UUID=...    /media/data    ntfs     defaults    0   2
```

重启应该就正常了

# 输入法
安装 fcitx 框架
```
sudo apt-get install fcitx-bin
sudo apt-get install fcitx-table
```
安装网上下载的搜狗输入法linux版 (Ubuntu有提供.deb)
重启电脑即可


>版权声明： 本博客所有文章除特别声明外，均采用[CC BY-NC-SA 3.0 CN](https://creativecommons.org/licenses/by-nc-sa/3.0/cn/deed.zh)许可协议。转载请注明出处！
