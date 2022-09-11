---
layout:  post
id:  1534
title:  "linux系统使用cloud-init脚本开启root账号密码登录"
slug:  "linux下使用cloud-init脚本开启root账号密码登录"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2019-09-22 20:29:17
---



<ul>
 	<li>脚本如下：</li>
</ul>
<pre class="prettyprint">#!/bin/bash
echo root:Joker |sudo chpasswd root
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
sudo service sshd restart</pre>
<ul>
 	<li>默认密码是：Joker</li>
</ul>