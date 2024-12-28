---
title: 赛马娘繁中URA配置记录
aside: true
tags:
  - 网络
description: 赛马娘URA配置
categories: 日常
abbrlink: e59d5e35
date: 2024-06-28 18:03:52
updated: 2024-12-29 04:11:02
---


# 前言
UmamusumeResponseAnalyzer（后文简称URA）是一个赛马娘工具，项目地址为：
https://github.com/UmamusumeResponseAnalyzer/UmamusumeResponseAnalyzer
# 本文使用的工具版本

- 雷电模拟器9 {% label 国内版v9.0.61 blue %} [官网地址](https://www.ldmnq.com/other/version-history-and-release-notes.html)
- Kitsune Magisk（原名Magisk Delta）{% label  v26-1 red %}[官网地址](https://huskydg.github.io/magisk-files/ )，博主本人是在该[网站]( https://magisk-delta.en.uptodown.com/android)下载的旧版，可以自行前往其他可信任的网站下载
- Localify模块：zygisk-umamusume-localify-2.16.2.with.vanilla.msgpack.hook-release.zip [下载地址](https://github.com/UmamusumeResponseAnalyzer/umamusume-localify-android/releases)
- 用于设置localify的apk：Localify Settings v1.6.0 [下载地址](https://github.com/Kimjio/umamusume-localify-android/releases)
- UmamusumeResponseAnalyzer：v1.13.2.2 [下载地址](https://github.com/UmamusumeResponseAnalyzer/UmamusumeResponseAnalyzer/releases)
- 赛马娘谷歌版：前往[官网](https://uma.komoejoy.com/)获取，或者使用qooapp、apkpure、apkcombo等第三方软件获取
# 从零开始的安装过程
## 模拟器下载设置

1. 雷电官网下载安装上述版本
2. 把`System.vmdk`和`Root`打开
3. 重启模拟器

## APP下载和文件操作
### 文件下载
下载安装Kitsune Magisk、Localify Settings和赛马娘繁中**谷歌版**
下载zygisk-umamusume-localify-2.16.2.with.vanilla.msgpack.hook-release.zip并拖入模拟器，放进共享文件夹中
### Magisk设置

1. 打开Kisune Magisk，勾选**永久允许Root**，点击Magisk旁边的安装，勾选**允许访问文件**
2. 重点来了：***关闭并重启Magisk*** ，否则可能导致“安装到系统分区”不存在
3. 再次点击Magisk旁边的安装，第一步的选项**不要勾选**，第二步选择**安装至系统分区**，如图所示：![](../images/dea47f18cf40dc9c93b60819f073904c.png) ![](../images/caf5dd1164e5cf2a5c5197a6583d913e.png)
4. 直接使用点击**模拟器右上角的重启**，**不要**使用Magisk的重启
5. 打开Magisk进入设置勾选Zygisk，返回，打开模块，选择从本地安装，进入共享文件夹（一般是Pictures），确认安装，**重启**（还是一样，使用模拟器的重启）

### Localify的设置

1. 下载安装**赛马娘谷歌版**，运行游戏，到了登录界面就可以退出了，这步是为了生成Android/data/里的游戏数据文件
2. 打开Locatify Settings，软件会自动选择赛马娘游戏文件夹，点击选择就好，正常情况如图所示：![](../images/bfd49008470e900bc7c441470cb5ac2d.png)
3. 点击Dump MessagePack，打开开关，点击Notifier host，输入你的本机IP:4693（通常为局域网IP，如博主是`http://192.168.2.185:4693`）
   如何获取IP？按Win+R，输入cmd打开命令行，输入`ipconfig`，找到你的ipv4地址即可

## 电脑端软件下载
1. 下载URA本体，使用**管理员权限启动**
2. 选择菜单中的更新数据
3. 选择启动，出现IP地址和已启动字样即为成功
4. 验证连接：打开模拟器的浏览器，输入 http://ip:4693/notify/ping ，如果连接正常，会有正确信息输出，如图所示：![浏览器里的输出是pong](../images/b36af439471dee46bfcf2b9e5073a352.png)

# 常见问题
-  Localify Settings中找不到赛马娘数据文件夹：首先看有没有忘记打开赛马娘，进入到登录界面，其次看赛马娘版本，应使用**谷歌版**而不是mycard版
- URA报错：自行查询项目issue，博主使用最新版的数据测试一切正常，如果需要使用旧版本，可以自行前往Release下载exe，并在QQ频道等渠道获取旧版本的br数据文件
- 事件成功失败不显示：URA设置中打开selectindex，输出@1就是成功，@2则是失败
- 赛马娘闪退：可能是模块问题、模拟器问题、游戏问题。按照顺序来：
  1. 关闭Localify模块，清除游戏缓存，重启游戏，确认能正常进入后再打开模块开关
  2. 重启模拟器，群友：修改模拟器为单核可改善闪退（博主未验证）
  3. 尝试重装游戏，可换个安装包，还不行那就重装模拟器
- 其余问题：~~重启解决90% 重装解决99%~~


#  凯旋门版本问题
2024年12月凯旋门版本更新后出现bug，导致URA无法正常使用。
P.S. 博主本人是从apkpure上直接下载v2.0.3版本并直接安装。

## 问题排查

adb排查发现：arm64-v8a.so出现问题 ![](../images/Pasted%20image%2020241229034252.png)
近期台服1.35.0版本首次使用了.xapk打包，博主此时猜测为兼容性问题，拆开近期更新的两个版本.xapk外加对比apkpure上的架构词条：[v1.35.0](https://apkpure.com/cn/%E8%B3%BD%E9%A6%AC%E5%A8%98pretty-derby/com.komoe.kmumamusumegp/download/1.35.0) 为`arm64-v8a`， [v2.0.3](https://apkpure.com/cn/%E8%B3%BD%E9%A6%AC%E5%A8%98pretty-derby/com.komoe.kmumamusumegp/download/2.0.3) 为`armeabi-v7a`
而旧版本[v1.34.0](https://apkpure.com/cn/%E8%B3%BD%E9%A6%AC%E5%A8%98pretty-derby/com.komoe.kmumamusumegp/download/1.34.0)（.apk打包）则为`arm64-v8a,armeabi-v7a`
可以发现：新版本采用.xapk打包，导致模拟器安装后出现兼容性问题，致使URA无法正确调用.so库

## 解决方案
下载{% label v1.34.0 blue %}或更旧版本的**谷歌版**安装包，安装后使用{% label qooapp red %}进行更新。
*v1.35.0版本或许也可以，暂未测试* 