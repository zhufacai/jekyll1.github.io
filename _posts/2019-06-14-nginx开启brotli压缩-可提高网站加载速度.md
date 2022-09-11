---
layout:  post
id:  1417
title:  "宝塔面板Nginx下开启Brotli压缩，可提高网站加载速度"
slug:  "nginx开启brotli压缩-可提高网站加载速度"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2019-06-14 19:09:00
---



说明：<strong>Brotli</strong>是<strong>Google</strong>推出的开源压缩算法，通过变种的<strong>LZ77</strong>算法、<strong>Huffman</strong>编码以及二阶文本建模等方式进行数据压缩，与其他压缩算法相比，它有着更高的压缩效率，性能也比我们目前常见的<strong>Gzip</strong>高<strong>17-25%</strong>，可以帮我们更高效的压缩网页中的各类文件大小及脚本，从而提高加载速度，提升网页浏览体验。
1、下载Brotli
<pre class="prettyprint">cd /www/server
#下载brotli
git clone https://github.com/google/ngx_brotli.git
cd ngx_brotli
#更新brotli
git submodule update --init</pre>
2、编译Nginx

先查看目前Nginx的版本信息：
<pre class="prettyprint">nginx -V</pre>
输出以下信息：
<pre class="prettyprint">[root@Joker ~]# nginx -V
nginx version: nginx/1.15.10
built by gcc 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) 
built with OpenSSL 1.1.1b  26 Feb 2019
TLS SNI support enabled
configure arguments: --user=www --group=www --prefix=/www/server/nginx --with-openssl=/www/server/nginx/src/openssl ... --with-ld-opt=-ljemalloc</pre>
Nginx版本为1.15.10，configure arguments:后面的为你nginx的编译参数，下面会用到。

然后重新下载nginx，并开始编译，使用命令：
<pre class="prettyprint">#下载nginx，这里下载的1.15.10版本，如果是其它版本，把下载链接的1.15.10改成你的版本号即可
wget http://nginx.org/download/nginx-1.15.10.tar.gz
#解压并删除压缩包
tar -xvzf nginx-*.tar.gz &amp;&amp; rm -rf nginx-*.tar.gz
#进入nginx目录
cd nginx*
#生成Makefile，./configure后面的参数直接复制上面看到的，然后在后面额外加一个--add-module=/www/server/ngx_brotli
./configure --user=www --group=www --prefix=/www/server/nginx ... --add-module=/www/server/ngx_brotli
#编译nginx
make &amp;&amp; make install</pre>
编译完成，然后继续使用命令查看信息:
<pre class="prettyprint">nginx -V</pre>
返回参数后面多了个`--add-module=/www/server/ngx_brotli`就表示编译成功了。

 3. 开启Brotli压缩

接下来点击面板左侧软件商店-Nginx设置-配置修改，在http段内添加以下内容来启用Brotli压缩。
<pre class="prettyprint">brotli on;
brotli_comp_level 6;
brotli_min_length 512;
brotli_types text/plain text/javascript text/css text/xml text/x-component application/javascript application/x-javascript application/xml application/json application/xhtml+xml application/rss+xml application/atom+xml application/x-font-ttf application/vnd.ms-fontobject image/svg+xml image/x-icon font/opentype;
brotli_static always;</pre>
最后点击Nginx设置里的重载配置生效即可。
<ul>
 	<li>
Brotli全部参数详解：
</li>
</ul>
<pre class="prettyprint">brotli on;              #启用
brotli_comp_level 6;    #压缩等级，默认6，最高11，太高的压缩水平可能需要更多的CPU
brotli_buffers 16 8k;   #请求缓冲区的数量和大小
brotli_min_length 20;   #指定压缩数据的最小长度，只有大于或等于最小长度才会对其压缩。这里指定20字节
brotli_types text/plain application/javascript application/x-javascript text/javascript text/css application/xml text/html application/json image/svg application/font-woff application/vnd.ms-fontobject application/vnd.apple.mpegurl image/x-icon image/jpeg image/gif image/png image/bmp;   #指定允许进行压缩类型
brotli_static always;   #是否允许查找预处理好的、以.br结尾的压缩文件，可选值为on、off、always
brotli_window 512k;     #窗口值，默认值为512k</pre>
&nbsp;


  [1]: https://www.joker.cc/usr/uploads/2020/12/1336622056.png