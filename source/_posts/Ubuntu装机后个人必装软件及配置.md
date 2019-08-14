---
title: Ubuntu装机后个人必装软件及配置
date: 2018-06-19
tags: [Ubuntu]
---

# Ubuntu 18 版本  

## google-chrome

```bash

sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/

wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable
```

安装完成之后，命令行启动

`/usr/bin/google-chrome-stable`

启动完成之后锁定到启动器即可。

## shadowsocks-qt5

```bash
sudo add-apt-repository ppa:hzwhuang/ss-qt5

sudo apt update

sudo apt install shadowsocks-qt5 -y
```

Ubuntu18及以上版本会在`add-apt-repository`之后会报错，需要手动去改版本信息：

打开文件：

```
sudo vi /etc/apt/sources.list.d/hzwhuang-ubuntu-ss-qt5-cosmic.list
```

将下面 `xenial`改成`cosmic`:

```

deb-src http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu xenial main

```

## ssr-qt5与全局代理

[参考这里](https://www.litcc.com/2016/12/29/Ubuntu16-shadowsocks-pac/index.html)

```bash
sudo pip install genpac
pip install --upgrade genpac
```

### 下载规则

https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt 保存到本地gfwlist.txt

在fwlist.txt 目录下，执行以下命令：

```bash
genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" --gfwlist-local=gfwlist.txt --output="autoproxy.pac"
```

### 设置全局代理

点击：System settings > Network > Network Proxy，选择 Method 为 Automatic，设置 Configuration URL 为 autoproxy.pac 文件的路径，点击 Apply System Wide。
格式如：file:///home/{user}/autoproxy.pac

file:///home/ouou/Downloads/autoproxy.pac

## unity-tweak-tool

```bash
sudo apt-get install unity-tweak-tool
```

<!--more-->

## 网易云音乐

~~ 下载地址：[V1.1.0](http://d1.music.126.net/dmusic/netease-cloud-music_1.1.0_amd64_ubuntu.deb) ~~
官网更新的1.1.0版本安装完成之后，之后超级管理员能够启动，普通管理员无权限，所以要安装1.0.0版本的。

[V1.0.0](http://s1.music.126.net/download/pc/netease-cloud-music_1.0.0_amd64_ubuntu16.04.deb)

下载完成之后，在文件所在目录：

```
sudo dpke -i netease-cloud-music_1.0.0_amd64_ubuntu16.04.deb
```

## WPS for Linux

官网下载安装包[http://kdl.cc.ksosoft.com/wps-community/download/6634/wps-office_10.1.0.6634_amd64.deb](http://kdl.cc.ksosoft.com/wps-community/download/6634/wps-office_10.1.0.6634_amd64.de)

下载完成之后，进行安装

```bash
sudo dpkg -i wps-office_10.1.0.6634_amd64.deb

# 以下是卸载libreOffice
sudo apt-get remove libreoffice-common

sudo apt-get remove unity-webapps-common

sudo apt autoremove
```

### 字体缺失问题

下载字体包：

[https://pan.baidu.com/s/1eS6xIzo](https://pan.baidu.com/s/1eS6xIzo)

下载之后解包，然后

```bash
sudo cp mtextra.ttf  symbol.ttf  WEBDINGS.TTF  wingding.ttf  WINGDNG2.ttf  WINGDNG3.ttf  /usr/share/fonts
```

重启wps 即可。

## 安装MAC字体

```bash
wget -O mac-fonts.zip http://drive.noobslab.com/data/Mac-14.04/macfonts.zip

sudo unzip mac-fonts.zip -d /usr/share/fonts; rm mac-fonts.zip

sudo fc-cache -f -v
```

## 状态栏显示网速

```bash
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install indicator-netspeed
```

之后把 `indicator-netspend` 加入到自动的脚本中去。[参考](https://blog.csdn.net/sinat_36219858/article/details/61195905)

## 搜狗输入法

## 美化终端

### 安装zsh
### 安装terminator
## Vim 安装

** 以上的三个配置为了方便移至，已经写了一个自动部署的脚本，详见[ubuntu_auto_config](http://github.com/suadminwen/ubuntu_auto_config) **

脚本完成之后，配置基本完成。

## 截屏软件

安装`deepin-screenshot`
先安装一些必须安装的库

```
sudo apt install python-deepin-utils python-imaging python-scipy python-wnck python-xdg
```

下载安装包进行安装：

```
wget http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-utils/python-deepin-utils_0.0.1-1%2bgit20130502093354ubuntu2_amd64.deb \
         http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-gsettings/deepin-gsettings_0.1%2bgit20130318115600ubuntu1_amd64.deb \
         http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-ui/deepin-ui_1%2bgit20130618094833~90b6485f6cprecise2_all.deb \
         http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-screenshot/deepin-screenshot_2.0%2bgit20130618155753~8c1ba38453precise_all.deb

sudo dpkg -i python-deepin-utils_0.0.1-1+git20130502093354ubuntu2_amd64.deb 
sudo dpkg -i deepin-gsettings_0.1+git20130318115600ubuntu1_amd64.deb
sudo dpkg -i deepin-ui_1+git20130618094833~90b6485f6cprecise2_all.deb
sudo dpkg -i deepin-screenshot_2.0+git20130618155753~8c1ba38453precise_all.deb
```
安装的过程中，如果出现**依赖关系问题 - 仍未被配置**等问题，执行`sudo apt -f install `之后重新执行安装命令即可。

安装完成之后，在终端输入命令`deepin-screenshot`就会出现截屏的界面，然后自定义快捷键`ctrl+alt+a`启动截屏
