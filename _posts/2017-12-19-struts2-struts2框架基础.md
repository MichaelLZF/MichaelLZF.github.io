---
layout:     post
title:      struts2框架基础
subtitle:
date:       2017-12-19
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - struts2
---

# 说明
以下内容为初学struts2的体会，该框架的深入使用还未了解

## struts2工作流程

1.客户端提交一个HttpServletRequest请求；

2.请求被提交到一系列filter：ActionContextCleanUp-->SiteMesh-->FilterDispatcher；

3.FilterDispatcher收到请求后，询问ActionMapper是否需要调用某个action来处理http请求，如果需要，则将请求交给ActionProxy；

4.ActionProxy通过Configuration Manager（struts.xml）询问框架的配置文件，找到需要调用的action类；

5.ActionProxy创建一个ActionInvocation实例，同时，ActionInvocation通过代理模式调用Action，在调用之前，ActionInvocation会根据配置加载所有action配置的拦截器（interceptor）；

6.action执行完毕，ActionInvocation负责根据struts.xml中的配置找到对应的返回<result>,然后将返回对应的视图呈现给客户端。

## struts2所需jar包

```swift
//基本jar包

1.struts2-core

2.xwork

3.freemarker

4.ognl

5.commons-logging

6.commons-lang

7.commons-lang3

//文件上传

8.commons-io

9.commons-fileupload

//java编程助手，使Java字节码操纵简单

10.javassist

```

## web.xml配置

该页面可以配置struts2启动服务器后要访问的首页面；

1.在`<welcome-file>`中配置访问路径即可，当文件在`WebContent`路径下时，直接写文件名即可，若在`webcontent`文件下的子文件夹下，添加子文件夹的路径；

2.filter配置如下
```swift
	<filter>
      <filter-name>struts2</filter-name>
      <filter-class>
        <!--org.apache.struts2.dispatcher.FilterDispatcher 该分发器不再使用 --> 
         org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter
      </filter-class>
   </filter>

   <filter-mapping>
      <filter-name>struts2</filter-name>
      <url-pattern>/*</url-pattern>
   </filter-mapping>
```

## struts.xml配置

1.该文件需放置好在src目录下

2.具体配置

1）`<package>`该标签需要写出extends的值，一般都会继承struts-default；

2）`<action>`该标签是用来指出客户端请求后需要响应的动作，action的name需跟请求页面设置的action名称一致，如：`<form action="action中配置的名字"/>`

其次，class属性表明了该action对应的类

3）`<result>`该标签在`<action>`标签下，告诉action，当返回值为SUCCESS/ERROR/INPUT……之后，需要跳转/执行的操作。

4）还可以配置一些其他的属性，如拦截器`<interceptor>`

## logging.properties

```swift
org.apache.catalina.core.ContainerBase.[Catalina].level = INFO
org.apache.catalina.core.ContainerBase.[Catalina].handlers = \
                              java.util.logging.ConsoleHandler
```
日志配置文件

## struts.properties

存放一些key-value对，可以修改struts默认配置的一些常量值
如：上传文件时，默认最大为2M，可以修改该文件中的`struts.multipart.maxSize=50000000000`增加上传文件的大小

## Action类

1.可以直接在Action类中定义对象的属性，但是不便于管理，因此，一般单独创建对象model，在action类中创建model对象，再获取其属性；

2.execute()方法：如果在struts.xml的<result>标签中未指明method的值，则会默认执行execute中的动作。

