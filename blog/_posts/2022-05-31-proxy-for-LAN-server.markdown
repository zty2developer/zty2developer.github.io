---
layout: post
title:  "Set Proxy For server in LAN"
date:   2022-05-31 15:39:54 +0800
categories: Others
---

{% highlight shell %}
# 以下所有操作都在服务器上进行
sudo apt install squid
sudo service squid start

# xx是自己的本机ip
export http_proxy="xx:3128"  
export https_proxy="xx:3128"

# 新建文件
vim /etc/apt/apt.conf.d/98https-http-proxy
# 在里面写入:
Acquire::http::Proxy "http://xx:7890";
Acquire::https::Proxy "http://xx:7890";

# 验证服务器是否连上网
curl -l www.baidu.com

# 如果要通过apt安装软件记得换apt source
{% endhighlight %}

