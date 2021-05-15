---
title: 初次尝试为Mi2编译AOSP11
categories:
  - 开发
  - Android
tags:
  - AOSP
  - Mi2
date: 2021-05-14 22:33:11
updated: 2021-05-14 22:33:11
---

## TL; DR

今年五一面基时，跟 [TH779](https://github.com/hh2333) 聊天时 ~~莫名其妙地~~ 谈起了Mi 2，我这个追求高版本号的人便问起：“这 ~~破~~ Mi2有大佬给适配AOSP11嘛”

779于是指路 乖奕虎 的[项目](https://github.com/tiger-cave/local_manifests)

于是……

> 刚才有个朋友 ~~(TH779)~~ 问我
> 
> "莳老师，发生什么事啦"
>
> 我说怎么回事
>
> 给我发了几个链接
>
> 我一看
>
> 哦
> 
> 原来是乖奕虎佬已经写好了编译方法
>
> 我说那我肯定得试试啊
>
> 我一说他啪一下就站起来了 ~~_『他』不指任何一个人_~~
>
> 很快啊
>
> 然后上来就是
>
> 一晚上sync
>
> 一小时checkout ~~_我忘了checkout用了多久了_~~
>
> 我全部等过去了啊
>
> 等过去以后自然是
>
> ```make -j8 otapackage```
>
> 我笑一下
>
> 准备睡觉
>
> 他突然一个ERROR出来袭击
>
> 啊
>
> 我大意了啊
>
> 我说停停
>
> 我说小伙子你不讲武德你不懂
>
> 后来他说他练过三四年AOSP啊
>
> 这个年轻人不讲武德
>
> 来骗来偷袭我这个69岁的老同志
>
> 这好吗
>
> 这不好
>
> 我劝这位年轻人
>
> **好自为之**

---

## 编译机

由一位不愿透露姓名的朋友提供

物理机: 3900X + 48G Ram

编译时使用虚拟机: 20 Virtual Cores + 32G Ram

采用 Ubuntu Desktop 18.04

## 拉取AOSP Repo

由于处在天朝的网络环境下，我选择了TUNA提供的AOSP镜像进行同步

![TUNA Mirror](https://i.loli.net/2021/05/15/4BxOiJ6CIEadGTv.png)

首先按照TUNA的[wiki](https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/)配置好repo工具

然后创建一个工作区文件夹

按照先后顺序执行

```
repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-11.0.0_r32

curl --create-dirs -L -o .repo/local_manifests/local_manifest.xml -O -L https://github.com/tiger-cave/local_manifests/raw/android-11.0/local_manifest.xml

repo sync
```

大概这样:

![Sync Repo](https://i.loli.net/2021/05/14/87F5bLEnYqirSkR.png)

~~因为连接GitHub实在是太慢了，我选择给Git挂上了代理~~

![Checkout](https://i.loli.net/2021/05/14/8nkDqCzKbhpiFoL.jpg)

_朋友那里的网络条件并不算好，这一步大概消耗了一晚上_

## 编译前准备

![Hu Repo](https://i.loli.net/2021/05/15/yptVoS4jT2BK3mh.png)

按照乖奕虎的文档，我们只需要执行如下的命令

```
. build/envsetup.sh

lunch aosp_aries-userdebug
```

![Start Build](https://i.loli.net/2021/05/14/rxiljvk6L8UH92D.jpg)

因为虚拟硬盘拉完Repo过后容量不太够，于是我加了一块，然后调整了 OUT_DIR 这个环境变量，字面意思，它指定了编译时输出的文件去哪里

```
export OUT_DIR=/media/sdltqlwscjddw/HDD/aosp-output
```

完成后再执行一下以下这条命令即可

```
lunch aosp_aries-userdebug
```

## 编译

目前为止，一切似乎都顺风顺水，那么编译也会吧！

我当时的确是这么想的

然后敲下

```
make -j8 otapackage
```

准备睡觉

没过几分钟跳出一条红色的ERROR

~~好像忘保存截图了~~

MD，不管了，先去睡觉

第二天，~~貌似779当时刚有空~~

一顿研究后，779说:

![TH779](https://i.loli.net/2021/05/15/REJIUyjc3Fk2wAq.png)

传送门: [tiger-cave/bionic](https://github.com/tiger-cave/bionic)

就是这样，重新运行，终于正常编译了

![Building](https://i.loli.net/2021/05/14/UgcRGMQSK3qauLp.jpg)

> 啪的一下
>
> 很快啊

一个多小时过后，编译完成啦

![Done](https://i.loli.net/2021/05/14/ZlEu6rpY3cbkRHC.jpg)

然后就是把刷机包传到我电脑这，刷进去试试

## 刷入

通过TWRP，我使用ADB Sideload成功地刷入了编译好的AOSP 11

![Try On](https://i.loli.net/2021/05/15/mVQn1ti6K9gkIbW.jpg)

~~然后体验并不是很舒服，所以我刷回了乖奕虎制作的Mokee10.0~~

~~过了这么久，总算是想起还没发包了~~

[OneDrive](https://shiro233-my.sharepoint.com/:u:/g/personal/shisheng_shiro233_onmicrosoft_com/EbL3ur0PMl9Htz5VmCy70wYBgRmUBFM7ivv_Kgfmgta2_Q?e=2pTyWe) 

MD5 Checksum: 192ACF6FAB57EA78445E33389205B4A3

快快刷入体验一下吧

---

## 后记

总而言之，这是次**非常奇怪**的体验

~~_特别是在编译时发现有Prebuilt的包_~~

[:-(](https://t.me/shisheng_no_jibunnihanashikakeru/209)

然后在编译完成后，刷进Mi2体验了一个小时左右就刷回了Mokee

但是，最最重要的是这个过程，有好朋友和大佬陪着我

一步一步地指点我操作，跟我一起欢呼编译成功等等等等

在此，特别感谢 提供编译机的朋友 TH779 $Sudoerz 以及看着我操作的大家

这虽然是一个非常低技术力的操作，但我认为记录下来也是很有意思的

以及，在此向所有制作刷机包的大佬们致敬

嘛，今天就这样啦