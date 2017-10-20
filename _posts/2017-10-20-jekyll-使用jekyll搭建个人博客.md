---
layout:     post
title:      使用jekyll搭建个人博客
subtitle:
date:       2017-10-20
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - jekyll
    - github
---


## 安装jekyll

1.下载并安装ruby：http://rubyinstaller.org/downloads/，此处，我下载的是Ruby 2.4.2-2（x64）
     安装时可勾选"Add Ruby executables to your PATH"，会自动配置完成环境变量
2.cmd 输入 ruby -v 如果显示版本，说明安装成功；
3.确保gem已经正确安装：gem -v 如果安装，会显示版本
4.安装jekyll：gem install jekyll

## jekyll搭建网站的目录结构

此时，就可以使用jekyll的相关命令了，在使用之前，先看一下jekyll网站的一般目录结构：
```swift
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _data
|   └── members.yml
├── _site
└── index.html
```
其中
```swift
_config.yml 保存配置数据
_includes  方便重用布局文件
_layouts 包裹在文章外部的模板
_posts 里面是我们所写的文章
_site 编译之后的文件，上传的git时，可以用.gitignore过滤掉
```

## jekyll常用命令

```swift
jekyll new myblog  该命令会在当前目录下创建一个myblog文件夹，有默认页面
cd myblog进入文件夹之后使用：
jekyll serve --watch 检测文档的变化，并重启jekyll服务，该服务（本地）可以通过localhost:4000访问
```
编译后的文件则都在_site文件夹里

我在编译的过程中还遇到了分页错误
此时用
```swift
gem install jekyll-paginate  安装相关文件即可正常执行
```

## 编辑md文件可能遇到的问题

我在编辑文件时，用记事本编辑，总遇到编码问题，jekyll识别的是ANSI，但是中文却是UTF-8，
最好是使用代码编辑器，设置好文件编码，然后再编辑器里面编辑，既方便又可以避免一些错误。

## 上传部署

使用github上传部署即可。参考[使用github搭建个人网站]()

