---
title: Genymotion Android模拟器
layout: post
---



# Genymotion Android模拟器

想试试用Charles对AndroidApp 抓包，谁知道模拟器这么难调试

记录一下

Genymotion网络为(NAT) 

用模拟器访问本机地址为 10.0.3.2

我的Charles代理端口为7777，所以就设置上了



Mac 上启用 Surge 后，虚拟机的「网络设置-代理」里填上对应的 IP 地址就可以让虚拟机也能走代理，如下图所示假定 Mac 里的代理设置是 127.0.0.1:6152，通过查看虚拟机的 IP 可以推断出 Mac 作为主机的 IP 是 10.211.55.2，代理设置里填写 10.211.55.2:6152 即可。