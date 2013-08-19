---
layout: post
title: "第一篇Octopress Blog"
date: 2013-08-19 18:39
comments: true
categories: 
- 随笔
autor: Hobo
---
{% codeblock Git command lang:ruby %}
git add .
git commit -m 'update'
git push origin master
{% endcodeblock %}

{% codeblock Rake command lang:objc %}
rake preview
rake generate
rake deploy

rake new_post["title"]

rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
{% endcodeblock %}


