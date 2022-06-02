---
layout: post
title:  "Connect to the internet using proxy for LAN server"
date:   2022-05-31 19:28:13 +0800
categories: jekyll update
---
**Proxy Server**: 自己的电脑

**Host**: 局域网服务器 

> 所以是局域网服务器用自己的电脑作为代理，访问互联网。



### 1.Prerequisite

- ProxyServer和Host都需要装好Squid
- Proxy Server需要能同时访问互联网和内网
- 如果Proxy Server是Windows需要检查防火墙设置，不然Host的HTTP请求会被Proxy Server的防火墙拦截。可以直接关闭Proxy Server的防火墙。



### 2.Operations on Proxy Server

```shell
# 安装squid，如果自己电脑是Windows的话自己去网上下载安装
sudo apt install squid
sudo service squid start

# 查看Squid运行状态
sudo systemctl status squid
```



### 3.Operations on Host 

```shell
sudo apt install squid
sudo service squid start

# 查看squid运行状态
sudo systemctl status squid

# xx是用作代理的本机ip
export http_proxy="xx:3128"
export https_proxy="xx:3128"

# 新建文件
vim /etc/apt/apt.conf.d/98https-http-proxy

# 在里面写入:
Acquire::http::Proxy "http://xx:3128";
Acquire::https::Proxy "http://xx:3128";

# 验证服务器是否连上网
curl -l www.baidu.com

# 联网后如果要通过apt或者pip安装软件记得换source
```

