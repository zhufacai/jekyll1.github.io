---
layout: post
cid: 1288
title: WordPress文章页表格(table)自适应宽度
slug: wordpress文章页表格table自适应宽度
date: 2019/03/28 11:17:17
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<ul>
 	<li>
<h6>以下面表格为例：</h6>
</li>
</ul>
<a href="https://www.joker.cc/1276.html" target="_blank" rel="noopener"><img class="aligncenter wp-image-1289 size-full" src="https://www.joker.cc/wp-content/uploads/2019/03/表格示例.png" alt="" width="1008" height="171" /></a>
<ul>
 	<li>
<h6>代码如下：</h6>
</li>
</ul>
<pre class="prettyprint">&lt;table style="table-layout: fixed;" border="1" width="100%" cellspacing="0" cellpadding="2"&gt;
&lt;thead&gt;
&lt;tr&gt;
&lt;th style="text-align: left;"&gt;网站&lt;/th&gt;
&lt;th style="text-align: left;"&gt;地址&lt;/th&gt;
&lt;th style="text-align: left;"&gt;描述&lt;/th&gt;
&lt;/tr&gt;
&lt;/thead&gt;
&lt;tbody&gt;
&lt;tr&gt;
&lt;td style="text-align: left;"&gt;免费接收短信&lt;/td&gt;
&lt;td style="text-align: left;"&gt;http://www.shejiinn.com&lt;/td&gt;
&lt;td style="text-align: left;"&gt;中国、缅甸&lt;/td&gt;
&lt;/tr&gt;
&lt;tr&gt;
……
&lt;/tr&gt;
&lt;/tbody&gt;
&lt;/table&gt;</pre>
<ul>
 	<li>
<h6>解释：</h6>
<h6></h6>
border：表格的线宽为1；cellspacing：表格内数据与表格间隔为0；cellpadding：单元格与单元格间隔为2。</li>
</ul>