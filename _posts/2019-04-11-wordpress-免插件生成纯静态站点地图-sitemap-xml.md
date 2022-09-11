---
layout:  post
id:  1337
title:  "WordPress 免插件生成纯静态站点地图（sitemap.xml）"
slug:  "wordpress-免插件生成纯静态站点地图-sitemap-xml"
categories:  "Codes"
tags:  ""
permalink:  "/archives/:slug.html"
author:  "Joker"
date:  2019-04-11 17:38:06
---



<ul>
 	<li>
<h6>部署</h6>
</li>
</ul>
1.代码如下
<pre class="prettyprint">&lt;?php
require('./wp-blog-header.php');
header("Content-type: text/xml");
header('HTTP/1.1 200 OK');
$posts_to_show = 1000;
echo '&lt;?xml version="1.0" encoding="UTF-8"?&gt;';
echo '&lt;urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" xmlns:mobile="http://www.baidu.com/schemas/sitemap-mobile/1/"&gt;'
?&gt;
     &lt;url&gt;
      &lt;loc&gt;&lt;?php echo get_home_url(); ?&gt;&lt;/loc&gt;
      &lt;lastmod&gt;&lt;?php $ltime = get_lastpostmodified(GMT);$ltime = gmdate('Y-m-d\TH:i:s+00:00', strtotime($ltime)); echo $ltime; ?&gt;&lt;/lastmod&gt;
      &lt;changefreq&gt;daily&lt;/changefreq&gt;
      &lt;priority&gt;1.0&lt;/priority&gt;
  &lt;/url&gt;
&lt;?php
/* 文章页面 */
$myposts = get_posts( "numberposts=" . $posts_to_show );
foreach( $myposts as $post ) { ?&gt;
  &lt;url&gt;
      &lt;loc&gt;&lt;?php the_permalink(); ?&gt;&lt;/loc&gt;
      &lt;lastmod&gt;&lt;?php the_time('c') ?&gt;&lt;/lastmod&gt;
      &lt;changefreq&gt;monthly&lt;/changefreq&gt;
      &lt;priority&gt;0.6&lt;/priority&gt;
  &lt;/url&gt;
&lt;?php } /* 文章循环结束 */ ?&gt;
&lt;?php
/* 单页面 */
$mypages = get_pages();
if(count($mypages) &gt; 0) {
    foreach($mypages as $page) { ?&gt;
    &lt;url&gt;
      &lt;loc&gt;&lt;?php echo get_page_link($page-&gt;ID); ?&gt;&lt;/loc&gt;
      &lt;lastmod&gt;&lt;?php echo str_replace(" ","T",get_page($page-&gt;ID)-&gt;post_modified); ?&gt;+00:00&lt;/lastmod&gt;
      &lt;changefreq&gt;weekly&lt;/changefreq&gt;
      &lt;priority&gt;0.6&lt;/priority&gt;
  &lt;/url&gt;
&lt;?php }} /* 单页面循环结束 */ ?&gt;
&lt;?php
/* 博客分类 */
$terms = get_terms('category', 'orderby=name&amp;hide_empty=0' );
$count = count($terms);
if($count &gt; 0){
foreach ($terms as $term) { ?&gt;
    &lt;url&gt;
      &lt;loc&gt;&lt;?php echo get_term_link($term, $term-&gt;slug); ?&gt;&lt;/loc&gt;
      &lt;changefreq&gt;weekly&lt;/changefreq&gt;
      &lt;priority&gt;0.8&lt;/priority&gt;
  &lt;/url&gt;
&lt;?php }} /* 分类循环结束 */?&gt;
&lt;?php
 /* 标签(可选) */
$tags = get_terms("post_tag");
foreach ( $tags as $key =&gt; $tag ) {
    $link = get_term_link( intval($tag-&gt;term_id), "post_tag" );
         if ( is_wp_error( $link ) )
          return false;
          $tags[ $key ]-&gt;link = $link;
?&gt;
 &lt;url&gt;
      &lt;loc&gt;&lt;?php echo $link ?&gt;&lt;/loc&gt;
      &lt;changefreq&gt;monthly&lt;/changefreq&gt;
      &lt;priority&gt;0.4&lt;/priority&gt;
  &lt;/url&gt;
&lt;?php  } /* 标签循环结束 */ ?&gt;
&lt;/urlset&gt;</pre>
2.将上述代码新建为sitemap.php文件，上传到网站根目录即可。

3.访问<a href="https://www.joker.cc/sitemap.php" target="_blank" rel="noopener noreferrer">你的域名/sitemap.php</a>即可生成sitemap.php
<ul>
 	<li>
<h6>伪静态</h6>
</li>
</ul>
1.Nginx

编辑已存在的Nginx伪静态规则，新增如下规则后(平滑)重启nginx即可：
<pre class="prettyprint">rewrite ^/sitemap.xml$ /sitemap.php last;</pre>
2.Apache

编辑网站根目录的 .htaccess ，加入如下规则:
<pre class="prettyprint">RewriteRule ^(sitemap)\.xml$ $1.php</pre>
做好伪静态规则后，就可以直接访问<a href="https://www.joker.cc/sitemap.xml" target="_blank" rel="noopener noreferrer">你的域名/sitemap.xml</a>看看效果了