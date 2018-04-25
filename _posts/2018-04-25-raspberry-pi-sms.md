---
layout: post
title: Raspberry Pi 树莓派收短信，转发至Telegram
date: 2018-04-25 20:44:08.000000000 +02:00
published: true
categories:
- 点点滴滴
tags:
- 树莓派
---

我有一个sim卡专门用来收短信，但是平时用的手机是iPhone，不能双卡，带两个手机又麻烦，
所以想通过树莓派收短信，然后转发到手机上。

这里用到的是[Gammu SMSD](https://wammu.eu/smsd/)，专门负责收发短信的服务

需要用的有硬件当然有树莓派，此外，需要一个usb网卡

关于usb网卡，提前在[这里](https://wammu.eu/phones/)查一下哪个型号可以支持

我用的是华为[E160E](https://wammu.eu/phones/huawei/3135/)

将usb网卡连上树莓派，打开命令行里


```shell
> lsusb

Bus 001 Device 010: ID 12d1:1003 Huawei Technologies Co., Ltd. E220 HSDPA Modem / E230/E270/E870 HSDPA/HSUPA Modem
Bus 001 Device 004: ID 0424:7800 Standard Microsystems Corp.
Bus 001 Device 003: ID 0424:2514 Standard Microsystems Corp. USB 2.0 Hub
Bus 001 Device 002: ID 0424:2514 Standard Microsystems Corp. USB 2.0 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

### 第一行Huawei就是我的网卡

> ls /dev/ttyUSB*

/dev/ttyUSB0  /dev/ttyUSB1

### 我用到的是1

> sudo apt-get install gammu

> gammu-config

# 设备号填/dev/ttyUSB1 ，根据你的配置适当调整
# port at19200 ， 不同网卡可能有不同设置

> gammu identify

这里可以再次确定设备号

> sudo apt-get install gammu-smsd

> sudo vim /etc/gammu-smsdrc

# 这里是我的配置，service是null，不对消息进行存储
# 如果需要存储，可以配置file, mysql等，详见官方文档
# RunOnReceive定义收到短信后执行的脚本
# https://wammu.eu/docs/manual/smsd/run.html

# Configuration file for Gammu SMS Daemon
# Gammu library configuration, see gammurc(5)
[gammu]
# Please configure this!
port = /dev/ttyUSB1
connection = at19200
# Debugging
#logformat = textall
# SMSD configuration, see gammu-smsdrc(5)
[smsd]
RunOnReceive = /home/pi/receive-sms.sh
service = null
logfile = syslog
# Increase for debugging information
debuglevel = 0
```

以下是`/home/pi/receive-sms.sh`:

```
#!/bin/sh
TOKEN=“XXXXX"
CHAT_ID=XXXX
URL="https://api.telegram.org/bot$TOKEN/sendMessage"
for i in `seq $SMS_MESSAGES` ; do
  eval "curl -s -X POST $URL -d chat_id=$CHAT_ID -d text=\"\${SMS_${i}_TEXT}\""
done
```

我在这里将短信发送到Telegram，需要用到TOKEN和CHAT_ID两个变量

打开[BotFather](https://telegram.me/botfather)
一步一步创建自己的bot，然后就可以找到TOKEN

![botfather](http://ww1.sinaimg.cn/large/6b38e7d5gy1fqphf5mc0kj20da06jgm9.jpg)

在telegram里找到刚刚创建的bot，发送一个消息
然后浏览器打开
`https://api.telegram.org/bot{TOKEN}/getUpdates`
把TOKEN替换成你的TOKEN
这个链接会返回聊天列表，找到你自己的username就可以看到CHAT_ID

直接运行`gammu-smsd`测试一下，随便找个网站验证一下手机号就行

想每次启动自动运行的话
`systemctl start gammu-smsd.service`
