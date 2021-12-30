---
banner_img: /images/uploads/wallhaven-g8wvm7.webp
index_img: /images/uploads/1616421416500-wallhaven-rddv31.jpg
sticky: -2
title: Oracle Cloud控制面板开放端口
date: 2021-12-30 19:41:50
updated: 2021-12-30 19:41:50
tags:
  - Oracle Cloud
categories:
  - Oracle Cloud
keywords:
  - Oracle
excerpt:
  - Oracle Cloud
comments: true
---
<!--StartFragment-->

\## Oracle Cloud控制面板开放端口

\### ROOT操作



\`\`` bash

sudo su

\`\``

\### 处理预设规则

\`\`` bash

iptables -D INPUT -j REJECT --reject-with icmp-host-prohibited

iptables -D FORWARD -j REJECT --reject-with icmp-host-prohibited

/etc/init.d/netfilter-persistent save

/etc/init.d/netfilter-persistent reloa

\`\``

截至此处全部端口开放，无防火墙需求不用继续

\### 添加自定义规则

\`\`` bash

ufw enable #需要输入Y确认



ufw allow 22/tcp #开放22/tcp端口



ufw allow 80,443/tcp #开放80/tcp和443/tcp端口



ufw allow 1234/udp #开放1234/udp端口



ufw reload #重载防火墙

\`\``

<!--EndFragment-->