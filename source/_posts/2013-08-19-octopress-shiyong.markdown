---
layout: post
title: "Octopress 使用"
date: 2013-08-19 18:39
comments: true
categories: 
- 工具
autor: Hobo
---
{% codeblock Git command lang:ruby %}
git add .
git commit -m 'update'
git push origin master
{% endcodeblock %}

{% codeblock Rake command lang:objc %}
#预览
rake preview
#发布
rake generate
rake deploy

#创建文章
rake new_post["title"]

rake new_page[super-awesome]
# creates /source/super-awesome/index.markdown
rake new_page[super-awesome/page.html]
# creates /source/super-awesome/page.html
{% endcodeblock %}


