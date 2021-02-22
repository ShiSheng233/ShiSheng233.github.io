---
title: 记一次为了体验新版KDE而安装Arch
date: 2021-02-22 21:46:38
categories: 
	- 开发
	- Linux
tags: 
	- Arch Linux
	- KDE
---

~~其实我是来传教的~~

> 不建议小白在未做好心理准备的情况下尝试
>
> 请有一点耐心，因为你可能需要1145141919810小时~~也不能成功~~
> 
> **本文并不会教你安装Arch，只是记录一下**

![成品](https://cdn.jsdelivr.net/gh/ShiSheng233/ShiSheng233.github.io@gh-pages/images/Arch/Done.png)

## 准备

1. 镜像

鉴于中国的互联网形式，我推荐在镜像站[Tuna](https://tuna.moe)获取

2. 教程

~~只能~~推荐神一般的[Arch Wiki](https://wiki.archlinux.org/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

*由于Arch滚动更新等特性，我不建议在网络中查找安装他人的安装记录并效仿*

3. 安装好Arch Linux

![安装中](https://cdn.jsdelivr.net/gh/ShiSheng233/ShiSheng233.github.io@gh-pages/images/Arch/Installing.png)

## 开始安装KDE5.2.1

1. 混成窗口管理器

- Xorg
- Wayland

我 ~~因为不会配置Wayland~~ 选择了Xorg

```bash
$ sudo pacman -S xorg xorg-server
```

2. 硬件驱动

```bash
#显示#
$ sudo pacman -S xf86-video-intel  #Intel#
$ sudo pacman -S xf86-video-ati    #AMD#

#声音#
$ sudo pacman -S alsa-utils pulseaudio pulseaudio-alsa

#输入#
$ sudo pacman -S xf86-input-libinput
$ sudo pacman -S xf86-input-synaptics  #触控板#

#记得启用服务#
```

3. 登录管理器

- SDDM (KDE 默认 ~~现充~~)
- ~~KDM (KDE *曾经的* 默认)~~
- GDM (Gnome 默认)
- XDM  (Xorg 默认)
- ...

为了获取 **极致** 的 KDE5体验，我选择了SDDM

```bash
$ sudo pacman -S sddm sddm-kcm
$ systemctl enable sddm
```

4. 主角KDE&KDE-Applications

```bash
$ sudo pacman -S plasma kde-applications
```

**别忘了创建有root权限的账号！**

## 开始KDE5.2.1之旅

1. 重启

```bash
$ reboot
```

2. 好耶

![登录页面](https://cdn.jsdelivr.net/gh/ShiSheng233/ShiSheng233.github.io@gh-pages/images/Arch/Login.png)

*现在好像也不是很好看，但是这是你自己可以改的啦！*

![桌面](https://cdn.jsdelivr.net/gh/ShiSheng233/ShiSheng233.github.io@gh-pages/images/Arch/Desktop.png)

## 总结

我最初的目的是体验新的KDE，却又花了一上午安装Arch，操作CLI固然很繁琐，但能体会到折腾的乐趣。

用这么长的时间部署最难安装的Arch，我想，是值得的，哦，我的老伙计，我是说，我对上帝发誓，还蛮好玩的。

---

本文同时发布于[DrBlackの锦里](https://www.drblack-system.com/?p=2796)
