---
layout: post
cid: 1534
title: linux系统使用cloud-init脚本开启root账号密码登录
slug: linux下使用cloud-init脚本开启root账号密码登录
date: 2019/09/22 20:29:17
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
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