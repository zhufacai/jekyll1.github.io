---
layout: post
cid: 1346
title: WordPress显示网站运行时间
slug: wordpress显示网站运行时间
date: 2019/04/13 10:59:15
updated: 2020/12/16 20:12:54
status: publish
author: Joker
categories: 
  - Codes
tags: 
---


<ol>
 	<li>
<h6>显示效果：X<strong> </strong>天/X小时/X分/X秒，代码如下：</h6>
<!--?prettify linenums=true?-->
<pre class="prettyprint">&lt;span id="timeDate"&gt;载入天数...&lt;/span&gt;&lt;span id="times"&gt;载入时分秒...&lt;/span&gt;&lt;script&gt;// &lt;![CDATA[
var now = new Date(); function createtime(){ var grt= new Date("11/25/2013 21:51:00");//此处修改你的建站时间或者网站上线时间 now.setTime(now.getTime()+250); days = (now - grt ) / 1000 / 60 / 60 / 24; dnum = Math.floor(days); hours = (now - grt ) / 1000 / 60 / 60 - (24 * dnum); hnum = Math.floor(hours); if(String(hnum).length ==1 ){hnum = "0" + hnum;} minutes = (now - grt ) / 1000 /60 - (24 * 60 * dnum) - (60 * hnum); mnum = Math.floor(minutes); if(String(mnum).length ==1 ){mnum = "0" + mnum;} seconds = (now - grt ) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum); snum = Math.round(seconds); if(String(snum).length ==1 ){snum = "0" + snum;} document.getElementById("timeDate").innerHTML = "本站已安全运行"+dnum+"天"; document.getElementById("times").innerHTML = hnum + "小时" + mnum + "分" + snum + "秒"; } setInterval("createtime()",250);
// ]]&gt;&lt;/script&gt;</pre>
</li>
 	<li>
<h6>显示效果：X天，代码如下：</h6>
<!--?prettify linenums=true?-->
<pre class="prettyprint">本站已安全运行了:&lt;span class="smalltxt"&gt;&lt;script&gt;// &lt;![CDATA[
BirthDay=new Date("11 25,2013");
today=new Date();
timeold=(today.getTime()-BirthDay.getTime());
sectimeold=timeold/1000
secondsold=Math.floor(sectimeold);
msPerDay=24*60*60*1000
e_daysold=timeold/msPerDay
daysold=Math.floor(e_daysold);
document.write("&lt;font color=red&gt;"+daysold+"&lt;/font&gt;天 !");
// ]]&gt;&lt;/script&gt;&lt;/span&gt;</pre>
</li>
 	<li>
<h6>显示效果：X年X天X小时X分X秒，代码如下：</h6>
<!--?prettify linenums=true?-->
<pre class="prettyprint">&lt;span id="sitetime"&gt;&lt;/span&gt;&lt;script&gt;// &lt;![CDATA[
function siteTime(){ window.setTimeout("siteTime()", 1000); var seconds = 1000 var minutes = seconds * 60 var hours = minutes * 60 var days = hours * 24 var years = days * 365 var today = new Date() var todayYear = today.getFullYear() var todayMonth = today.getMonth() var todayDate = today.getDate() var todayHour = today.getHours() var todayMinute = today.getMinutes() var todaySecond = today.getSeconds() /* Date.UTC() -- 返回date对象距世界标准时间(UTC)1970年1月1日午夜之间的毫秒数(时间戳) year - 作为date对象的年份，为4位年份值 month - 0-11之间的整数，做为date对象的月份 day - 1-31之间的整数，做为date对象的天数 hours - 0(午夜24点)-23之间的整数，做为date对象的小时数 minutes - 0-59之间的整数，做为date对象的分钟数 seconds - 0-59之间的整数，做为date对象的秒数 microseconds - 0-999之间的整数，做为date对象的毫秒数 */ var t1 = Date.UTC(2013,11,25,21,30,20) var t2 = Date.UTC(todayYear,todayMonth,todayDate,todayHour,todayMinute,todaySecond) var diff = t2-t1 var diffYears = Math.floor(diff/years) var diffDays = Math.floor((diff/days)-diffYears*365) var diffHours = Math.floor((diff-(diffYears*365+diffDays)*days)/hours) var diffMinutes = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours)/minutes) var diffSeconds = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours-diffMinutes*minutes)/seconds) document.getElementById("sitetime").innerHTML=" 已运行"+diffYears+" 年 "+diffDays+" 天 "+diffHours+" 小时 "+diffMinutes+" 分钟 "+diffSeconds+" 秒" } siteTime()
// ]]&gt;&lt;/script&gt;</pre>
</li>
</ol>