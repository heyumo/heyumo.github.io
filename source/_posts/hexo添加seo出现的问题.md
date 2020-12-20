---
title: hexo添加seo出现过的问题
categories:
	
date: 2019-08-4 10:32:32
notshow: true
---

FATAL duplicated mapping key at line 70, column 18:
    path: sitemap.xml

    如果你的 hexo 版本是 2.x.x

    在_config.yml中添加如下代码：
    sitemap:
    path: sitemap.xml
	baidusitemap:
    path: baidusitemap.xml

    如果你的 hexo 版本是 3.x.x

	sitemap:
	path: sitemap.xml
	baidusitemap:
	path: baidusitemap.xml