---
layout: post
title: Sitemap.xml 만들기
---

* Github-Pages에서는 plug-in사용불가
* root 디렉토리 위치에 /sitemap.xml 파일생성

{% highlight js %}
---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {% for post in site.posts %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
      {% endif %}

      {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
      {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
      {% endif %}

      {% if post.sitemap.priority == null %}
          <priority>0.5</priority>
      {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
      {% endif %}

    </url>
  {% endfor %}
</urlset>
{% endhighlight %}

localhost:4000/sitemap.xml
홈페이지의 모든 글의 정보를 담고 있는 sitemap이 출력되는 것을 볼 수 있습니다.

sitemap에서 특정 글의 변경주기, 우선순위 정보를 변경하고 싶으면,
해당 글을 작성할 때 아래와 같이 lastmod, sitemap.chagefreq, sitemap.priority 정보를 추가하면 됩니다.

{% highlight md %}

---
layout: post
title:  "플러그인 없이 Jekyll Sitemap 만들기"
date:   2016-03-14 12:00:00
categories: Homepage
tags: sitemap.xml Jekyll Github-Pages
lastmod : 2016-03-15 12:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---
{% endhighlight %}

모든 글의 changefreq 를 짧게 주면 수많은 클로러들의 빈번한 접속에
Github-Pages가 힘들어할 수 있으니 중요한 변동이 없는 글들은 넉넉하게 잡아주세요.

## References

  * [generating-a-sitemap-in-jekyll-without-a-plugin](http://davidensinger.com/2013/03/generating-a-sitemap-in-jekyll-without-a-plugin/)
  * [havvg’s sitemap](https://github.com/havvg/havvg.github.com/blob/master/sitemap.xml)


