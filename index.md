---
layout: home
---

菜鸟 / 咸鱼 / 诗人→_→

记录每一个平凡的日落日升...


./Projects
----------

#### ./[Cloud][1]

#### ./etcd-cpp-apiv3

I maintain the de-facto C++ client library [etcd-cpp-apiv3][9] for [etcd][8]. The
library was first developed by nokia and open source under the BSD-3 License hasn't
been updated for years. I'm currently maintaining the library, and implemented features
like `watch`, `lease`, `lock` and enabled both token based and certificate based authentication,
I have also submitted a bunch of bug fixes as well.

After bringing the library to live again, it has received a lot of "thanks" from the
community.


./Writings
----------

I write blogs regularly at Github Pages to record things inspire me along the
way of coding.

<ul>
  {% for post in site.posts limit:6 %}
    <li class="alink">
      <a href="{{ post.url }}" class="red-link">
        {{ post.date | date: "%Y-%m-%d" }}&emsp;{{ post.title }}
      </a>
    </li>
  {%- endfor -%}
  <li class="alink"><a href="./blog/" class="red-link">&hellip;&hellip;</a></li>
</ul>



./Pageviews
-----------

[1]: https://cloud.joker.cc
[2]: https://gist.github.com/sighingnow/505d3d5c82237741b4a18147b2f84811
[3]: https://gist.github.com/sighingnow/96946f539342085a0759474d5389af7a
[4]: https://gist.github.com/sighingnow
[5]: https://summerofcode.withgoogle.com
[6]: https://osa1.net/
[7]: https://wiki.haskell.org/ThreadScope
[8]: https://etcd.io/
[9]: https://github.com/etcd-cpp-apiv3/etcd-cpp-apiv3
[10]: https://github.com/sighingnow/libclang
[11]: https://github.com/BHOSC
[12]: https://github.com/BHOSC/BUAAthesis
[13]: https://gist.github.com/sighingnow/dbe8b05483a786855e4d498019419cc4
[14]: https://gist.github.com/sighingnow/d0fb727c77f0d1e68143dd8157a30b0b
[15]: https://gist.github.com/sighingnow/9996851945408e8a960f81bf262260a1
[16]: https://gitlab.haskell.org/ghc
[17]: https://github.com/apache/arrow
[18]: https://github.com/pandas-dev/pandas
[19]: https://github.com/apache/incubator-mxnet
[20]: https://github.com/pytorch/pytorch
[21]: https://gist.github.com/sighingnow/4988a0100bc5030d301926f79254133a
[22]: https://github.com/sighingnow
[23]: https://www.youtube.com/watch?v=8fi7uSYlOdc
