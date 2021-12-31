---
title: Docker命令相关
categories: 
- Docker
tags:
- Docker
---


##  Docker命令相关

### Docker一键安装

``` bash
curl –sSL https://get.daocloud.io/docker | sh
```
### 查看运行容器


``` bash
docker ps
```
### 查看所有容器

``` bash
docker ps -a
```
### 进入容器

``` bash
docker exec -it CONTAINER /bin/bash
```
### 停用全部运行中的容器

``` bash
docker stop $(docker ps -q)
```
### 删除全部容器

``` bash
docker rm $(docker ps -aq)
```
### 一条命令实现停用并删除容器

``` bash
docker stop $(docker ps -q) & docker rm $(docker ps -aq)
```
