---
layout:  post
id:  1645
title:  "WordPress后台开启链接管理功能"
slug:  "wordpress后台开启链接管理功能"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2020-01-09 16:04:25
---



<ul>
 	<li>WordPress随着不断升级，在新版后台中取消了链接管理功能，可以通过一行代码重新开启这个功能，代码如下：</li>
</ul>
<pre class="prettyprint">add_filter( 'pre_option_link_manager_enabled', '__return_true' );</pre>
<ul>
 	<li>将上面代码添加到当前主题的<strong>functions.php</strong>中即可。</li>
</ul>