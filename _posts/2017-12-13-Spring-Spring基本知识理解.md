---
layout:     post
title:      Spring基本知识理解
subtitle:
date:       2017-12-13
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - Spring
    - IOC
    - AOP
---

## Spring

1.Spring是一个开源框架，为了解决企业应用开发的`复杂性`而创建的；它是一个轻量级的控制反转（IOC）和面向切面（AOP）的容器框架。

2.简要理解（优点）：
轻量级————从大小与开销两方面而言，Spring都是轻量级的；
松耦合————通过控制反转（IOC）达到松耦合的目的；
内聚性————允许通过分离应用的业务逻辑与系统服务进行内聚性的开发；
是一个容器————包含并管理应用对象的配置和生命周期；
是一个框架————将简单的组件配置、组合成为复杂的应用。
支持主流应用框架————对主流框架（Hibernate等）提供了良好的支持。

3.注意：
Spring不仅可以结合hibernate/mybatis等构件企业应用，还可以单独使用bean容器，单独使用AOP等其他Spring功能。

## 控制反转（IOC）

1.控制权的转移，应用程序本身不负责依赖对象的创建和维护，而是由外部容器负责创建和维护————获得依赖对象的过程被反转了。
2.DI（依赖注入）只是IOC的一种实现方式。

## 面向切面（AOP）

## bean的作用域
在Spring中，所有对象都是bean
1.singleton：单例，指一个Bean容器只存在一份。
2.prototype：每次请求创建新的实例，destroy方式不生效。
3.request：每次http请求创建一个实例，且仅在当前request内有效。
4.session：同上，每次http请求创建，仅在当前request内有效。
5.global session：基于portlet的web中有效，如果是在web中，同session。



