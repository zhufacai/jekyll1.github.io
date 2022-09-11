---
layout: post
cid: 1366
title: 基于宝塔Linux面板的shadowsocks可视化管理插件
slug: 基于宝塔linux面板的shadowsocks可视化管理插件
date: 2019/05/08 17:56:40
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<ul>
 	<li>
<h6>项目地址：<a href="https://github.com/Liang2580/btpanel-ss" target="_blank" rel="noopener">https://github.com/Liang2580/btpanel-ss</a></h6>
</li>
 	<li>
<h6>备用地址：<a href="https://github.com/404Joker/btpanel-ss" target="_blank" rel="noopener">https://github.com/404Joker/btpanel-ss</a></h6>
</li>
 	<li>
<h6>依赖主体：宝塔Linux面板</h6>
</li>
 	<li>
<h6>操作系统：Centos/Ubuntu</h6>
</li>
 	<li>
<h6>安装：</h6>
</li>
</ul>
<pre class="prettyprint">git clone https://github.com/404Joker/btpanel-ss.git

cd btpanel-ss

bash install.sh install</pre>
<ul>
 	<li>
<h6>卸载：先在可视化界面中删除所有用户端口,再执行以下命令</h6>
</li>
</ul>
<pre class="prettyprint">bash install.sh uninstall</pre>
<ul>
 	<li>
<h6>使用：直接登陆宝塔Linux面板 &gt;&gt; 打开软件列表页面 &gt;&gt; 转到列表最后一页即可看到新安装的shadowsocks插件</h6>
</li>
</ul>