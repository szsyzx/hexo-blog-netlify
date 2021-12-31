---
title: 设置Linux系统时间为北京时间
categories: 
- Linux
tags:
- Linux
---
## 设置Linux系统时间为北京时间

### 删除自带的localtime
``` bash
rm -rf /etc/localtime 
```
### 创建软链接到localtime
``` bash
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```
### 查看时间
``` bash
 date
```
