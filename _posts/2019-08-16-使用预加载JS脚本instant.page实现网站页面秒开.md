---
layout: post
cid: 1463
title: 使用预加载JS脚本instant.page实现网站页面秒开
slug: 实现网站页面秒开-预加载js脚本instant-page
date: 2019/08/16 17:22:34
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<ul>
 	<li>
<h6>原理</h6>
</li>
</ul>
使用即时预加载技术，在用户点击之前预先加载页面。当用户的鼠标悬停在一个链接上超过<strong> 65</strong> 毫秒时，浏览器会对此页面进行预加载，当用户点击链接后，就从预加载的缓存中直接读取页面内容，从而达到缩短页面加载时间的目的。
<ul>
 	<li>
<h6>使用方法</h6>
</li>
</ul>
1.使用官方脚本

只要把下面这行代码添加到网站的<code>&lt;/body&gt;</code>标签之前即可。（由于脚本托管在国外，只建议国外的朋友使用，国内的朋友加载官方的资源会比较慢）
<pre class="prettyprint">&lt;script src="//instant.page/1.2.2" type="module" 
integrity="sha384-2xV8M5griQmzyiY3CDqh1dn4z3llDVqZDqzjzcY+jCBCk/a5fXJmuZ/40JJAPeoU"&gt;&lt;/script&gt;</pre>
2.自主托管脚本

只需将<a href="http://instant.page/1.2.2" target="_blank" rel="noopener noreferrer">instant.page/1.2.2</a>这段 js文件 上传到自己服务器，然后在<code>&lt;/body&gt;</code>标签之前根据路径添加下面的代码即可（强烈建议服务器在国内的朋友使用）
<pre class="prettyprint">&lt;script src="`存放路径`/instantclick-1.2.2.js" type="module"&gt;&lt;/script&gt;</pre>
&nbsp;