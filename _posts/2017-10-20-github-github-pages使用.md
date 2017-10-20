---
layout:     post
title:      github pages使用
subtitle:
date:       2017-10-20
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - github
---

## 使用github pages
github提供了https://username.github.io  这个域名给用户，在建站的过程中，可以直接使用username.github.io作为 repository

这样的话 访问https://username.github.io  即可访问到github提供给用户的站点。

## 重定向域名
不过该站点无法被百度等搜索引擎解析到，如果需要，可以自己购买域名访问（例如阿里万网）

购买之后等域名被认证，然后解析域名
解析域名时：
新建两个`A`的规则，其中一个是`www`，另一个是`@`，这样可以保证被搜索引擎搜索到，

最后，在CNAME文件中添加够买的域名，例如`zhuofeili.top`;

其中，如果是使用jekyll配合github pages，在_config.yml中添加CNAME配置，就可以重定向到自己的域名了。



