---
title: windows安装redis并部署
date: 2023-02-17 00:50:14
tags:
---
@[TOC](windows下安装redis)

# 下载

>  windows版本：
>         https://github.com/MSOpenTech/redis/releases
>     Linux版本：
>         官网下载：
>             http://www.redis.cn/
>         git下载
>             https://github.com/antirez/redis/releases

我们现在讨论的是windows下的安装部署，目前windows下最新版本是：3.2.100。
下载地址，提供多种下载内容，
Redis-x64-3.2.100.msi是在windows下，最简单的安装文件，方便，直接会将Redis写入windows服务。
Redis-x64-3.2.100.zip是需要解压安装的，接下来讨论的是这种。
Source code (zip) 源码的zip压缩版
Source code (tar.gz) 源码的tar.gz压缩版
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724224623589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)


# 安装
## 解压安装
将下载的Redis-x64-3.2.100.zip 解压到某个地址。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724224749591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
## 启动命令
通过cmd指定到该redis目录。
使用命令：

    redis-server.exe

 启动服务

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724224819538.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
出现这种效果，表明启动服务成功。

启动另一个cmd，在该redis目录下，使用命令：

    redis-cli.exe

 启动客户端,连接服务器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724224846614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
出现这种效果，表明启动客户度成功。

# 部署
由于上面虽然启动了redis服务，但是，只要一关闭cmd窗口，redis服务就关闭了。所以，把redis设置为一个windows服务。
安装之前，windows服务是不包含redis服务的 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724224927798.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
## 安装为windows服务
安装命令: `redis-server.exe --service-install redis.windows.conf` 使用命令，安装成功，如图所以： 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724225013220.png)
最后的参数 `--loglevel verbose`表示记录日志等级
安装之后，windows目前的服务列表 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724225108160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
## 常用的redis服务命令
卸载服务：`redis-server --service-uninstall`

开启服务：`redis-server --service-start`

停止服务：`redis-server --service-stop`

重命名服务：`redis-server --service-name name`

重命名服务，需要写在前三个参数之后，例如：

> The following would install and start three separate instances of Redis as a service:    
> 以下将会安装并启动三个不同的Redis实例作服务：
> 
> redis-server --service-install --service-name redisService1 --port  10001
> 
> redis-server --service-start --service-name redisService1
> 
> redis-server --service-install --service-name redisService2 --port 10002
> 
> redis-server --service-start --service-name redisService2
> 
> redis-server --service-install --service-name redisService3 --port 10003
> 
> redis-server --service-start --service-name redisService3

# 测试
## 启动服务

    redis-server --service-start

## 客户端
命令：

    精简模式：
    redis-cli.exe
    指定模式：
    redis-cli.exe -h 127.0.0.1 -p 6379 -a requirepass
    (-h 服务器地址  -p 指定端口号 -a 连接数据库的密码[可以在redis.windows.conf中配置]，默认无密码)

## 测试读写数据
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724225708754.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)
安装测试成功。

# Redis桌面管理工具
## 推荐使用的桌面管理工具：
Redis Desktop Manager
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190724225838309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nwa2FuZ3RhMTI=,size_16,color_FFFFFF,t_70)

下载地址： 
https://redisdesktop.com/download 
每一个让你难堪的现在，都有一个你不努力的曾经。
