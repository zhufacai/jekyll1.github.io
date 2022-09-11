---
layout:  post
id:  1564
title:  "CentOS 开启 BBR 加速"
slug:  "centos-开启-bbr-加速"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2019-10-26 17:17:00
---



一、升级内核版本
--------

    1.先查看内核版本
<pre class="prettyprint">uname -r</pre>
      输出信息如下：
<pre class="prettyprint">[root@Joker ~]# uname -r

3.10.0-327.22.2.el7.x86_64</pre>
BBR 算法需要Linux 4.9 及以上内核 ，Cent OS 7 上的 Linux 内核是 3.10, 所以得先升级内核版本。
    2.安装 eprl 的源
<pre class="prettyprint">sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm</pre>
    3.安装最新的内核版本
<pre class="prettyprint">sudo yum --enablerepo=elrepo-kernel install kernel-ml -y</pre>
   4.修改 grub2 的启动项，设置启动之后选择最新的内核
<pre class="prettyprint">sudo egrep ^menuentry /etc/grub2.cfg | cut -f 2 -d \'</pre>
   5.启动顺序已经修改了，但是为了以防万一，还是设置一下选择第一个为默认启动项
<pre class="prettyprint">sudo grub2-set-default 0</pre>
   6.最后就可以重启机器
<pre class="prettyprint">sudo reboot</pre>
   7.再次登录机器查看内核版本，已经是最新版本                                                                                                                                                                                                                                                                                          
                                 

**二、使用一键脚本开启BBR**

<pre class="prettyprint">sudo wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh &amp;&amp; chmod +x bbr.sh &amp;&amp; ./bbr.sh</pre>
查看bbr是否成功开启
`lsmod | grep bbr`
