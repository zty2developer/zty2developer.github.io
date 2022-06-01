---
layout: post
title:  "Connect to the internet using proxy for LAN server"
date:   2022-05-31 19:28:13 +0800
categories: jekyll update
---
A Post

{% highlight ruby %}
# 以下所有操作都在服务器上进行
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

# 联网后如果要通过apt安装软件记得换apt source
{% endhighlight %}
