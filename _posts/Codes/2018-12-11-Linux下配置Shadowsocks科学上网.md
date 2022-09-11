---
layout: post
cid: 1048
title: Linux下配置Shadowsocks科学上网
slug: linux下部署科学上网以及实现bbr加速
date: 2018/12/11 01:10:28
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<h6>环境：CentOS7X64
1.下载脚本</h6>
<pre class="prettyprint">wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh</pre>
<h6>2.增加执行权限</h6>
<pre class="prettyprint">chmod +x shadowsocks-libev.sh</pre>
<h6>3.运行</h6>
<pre class="prettyprint">./shadowsocks-libev.sh 2&gt;&amp;1 | tee shadowsocks-libev.log</pre>
<h6><strong> 安装过程中会提示配置端口、密码、加密方式。</strong></h6>
<h6>4.卸载</h6>
<pre class="prettyprint">./shadowsocks-libev.sh uninstall</pre>
<h6>5.控制</h6>
启动： <!--?prettify linenums=true?-->
<pre class="prettyprint">/etc/init.d/shadowsocks start</pre>
停止：<!--?prettify linenums=true?-->
<pre class="prettyprint">/etc/init.d/shadowsocks stop</pre>
重启：<!--?prettify linenums=true?-->
<pre class="prettyprint">/etc/init.d/shadowsocks restart</pre>
查看状态：<!--?prettify linenums=true?-->
<pre class="prettyprint">/etc/init.d/shadowsocks status</pre>