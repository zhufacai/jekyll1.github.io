---
layout: post
cid: 1645
title: WordPress后台开启链接管理功能
slug: wordpress后台开启链接管理功能
date: 2020/01/09 16:04:25
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<ul>
 	<li>WordPress随着不断升级，在新版后台中取消了链接管理功能，可以通过一行代码重新开启这个功能，代码如下：</li>
</ul>
<pre class="prettyprint">add_filter( 'pre_option_link_manager_enabled', '__return_true' );</pre>
<ul>
 	<li>将上面代码添加到当前主题的<strong>functions.php</strong>中即可。</li>
</ul>