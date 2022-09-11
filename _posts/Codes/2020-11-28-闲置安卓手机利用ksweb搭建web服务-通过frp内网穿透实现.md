---
layout:  post
id:  1740
title:  "闲置安卓手机利用ksweb搭建web服务，通过frp内网穿透实现公网自定义域名访问"
slug:  "闲置安卓手机利用ksweb搭建web服务-通过frp内网穿透实现"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2020-11-28 18:15:00
---



一、安装ksweb搭建web服务
----------------

ksweb破解版：[点击下载][1]
1、下载ksweb安装并打开，通过简单的设置即可搭建web环境。
2、点击ksweb中显示的http://localhost:8080如能访问，证明ksweb安装成功并正常运行。
3、将所需的网站程序放置在ksweb显示的网站根目录下即可开始运行安装，此处不赘述。
4、安装成功后再次访问http://localhost:8080即可看到安装好的网站内容。

二、自建frp内网穿透
-----------

1、安装frp服务端
    apt-get update
    wget --no-check-certificate https://raw.githubusercontent.com/clangcn/onekey-install-shell/master/frps/install-frps.sh -O ./install-frps.sh
    chmod 700 ./install-frps.sh
    ./install-frps.sh install
之后会提示设置一些参数，全部参数都有默认值，直接回车就是输入默认值：
<pre class="prettyprint">Please input frps bind_port [1-65535](Default Server Port: 5443): #输入frp提供服务的端口，用于服务器端和客户端通信，默认即可
Please input frps vhost_http_port [1-65535](Default vhost_http_port: 80): #输入frp进行http穿透的http服务端口，建议选择其他端口，默认的80端口给Nignx，然后用Nginx代理frp的http端口
Please input frps vhost_https_port [1-65535](Default vhost_https_port: 443): #输入frp进行https穿透的https服务端口，同上面的80端口类似，建议分配其他端口，然后通过Nginx代理此端口
Please input frps dashboard_port [1-65535](Default dashboard_port: 6443):#输入frp的控制台服务端口，用于查看frp工作状态，默认即可
Please input dashboard_user (Default: admin):#登录控制台的用户名，默认即可
Please input dashboard_pwd (Default: kpkpM7VZ):#登录控制台的密码，如果记不住默认的建议修改
Please input privilege_token (Default: 9m2UAOWa6hx5Eise):#输入frp服务器和客户端通信的密码，默认是随机生成的，默认即可
Please input frps max_pool_count [1-200](Default max_pool_count: 50):#设置每个代理可以创建的连接池上限，默认50
##### Please select log_level #####
1: info
2: warn
3: error
4: debug
#####################################################
Enter your choice (1, 2, 3, 4 or exit. default [1]): 默认即可
Please input frps log_max_days [1-30](Default log_max_days: 3 day):
##### Please select log_file #####
1: enable
2: disable
#####################################################
Enter your choice (1, 2 or exit. default [1]):默认即可</pre>
安装完毕后会弹出以下内容，标明了具体信息，到此服务端操作全部完成。
<pre class="prettyprint">Congratulations, frps install completed!
==============================================
You Server IP      : 180.28.83.22
Bind port          : 5443
KCP support        : true
vhost http port    : 9080
vhost https port   : 9043
Dashboard port     : 6443
token              : LnDeMkeiIedDeDw
tcp_mux            : true
Max Pool count     : 50
Log level          : info
Log max days       : 3
Log file           : enable
==============================================
frps Dashboard     : http://180.28.83.22:6443/
Dashboard user     : admin
Dashboard password : admin
==============================================
frps status manage : frps {start|stop|restart|status|config|version}
/etc/init.d/frps {start|stop|restart|status|config|version}
Example:
  start: frps start
   stop: frps stop
restart: frps restart</pre>
此时可以访问ip地址+控制台端口进入frp控制台登录页面，通过前面设置的用户名和密码即可登录frp控制台。

2、安装frp客户端

frp安卓客户端下载：[点击下载][2]
（1）下载安装frp安卓客户端，配置客户端信息。
<pre class="prettyprint">[common]
server_addr = 180.28.83.22 #这里是服务器的IP
server_port = 5443 #服务器的连接端口
token = LnDeMkeiIedDeDw #服务器的连接Token

[web]
type = http
local_ip = 127.0.0.1
local_port = 8080
custom_domains = frp.joker.cc

[web1]
type = http
local_ip = 127.0.0.1
local_port = 8181
custom_domains = frp.joker.cc</pre>
配置完成后，保存。然后启动 frpc
（2）将 frp.joker.cc 的域名 A 记录解析到  180.28.83.22（此处更改为你的服务器公网IP），通过浏览器访问 http://frp.joker.cc:9080 即可看到到处于内网机器上的 web 服务。
（3）添加frp开机启动
在/etc/rc.local里面添加/home/frp/frps -c /home/frp/frps.ini (文件的具体路径根据实际情况填写),终端里面输入下面的命令，或者把文件下载回本地修改后重新上传覆盖源文件。
<pre class="prettyprint">vi /etc/rc.local</pre>

**三、反向代理**
<br>此时已经可以通过域名访问内网的web服务了，但是连接内网还是需要输入 9080端口，这时可以通过Nginx来反向代理实现通过80端口来访问。
1、Nginx新建一个虚拟主机配置，或者直接改默认的主机配置也可以。在Nignx 的listen 后 增加 default_server 配置，用来监听默认情况下所有来自解析到该服务器的域名
然后在 server 段内增加 反向代理配置。
<pre class="prettyprint">listen 80 default_server;

#frp proxy
location / {
proxy_set_header Host $host;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_pass http://127.0.0.1:9080;
}</pre>
这时候就可以通过 frp.joker.cc 来访问你内网的网站了。


  [1]: https://cloud.joker.cc/#s/6hyIDt0Q
  [2]: https://cloud.joker.cc/#s/6hyIgCyw