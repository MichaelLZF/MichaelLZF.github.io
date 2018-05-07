---
layout:     post
title:      Spring基础
subtitle:
date:       2017-12-19
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - hibernate
---

# 说明
以下内容为初学hibernate的体会，该框架的深入使用还未了解

## 什么是hibernate

1.hibernate是一个对象关系映射框架，是对JDBC的轻量级封装。基于这两个问题，所以在以下的jar包使用中，要使用到的至少包括hibernate相关包，以及数据库处理相关包。

2.关系和对象的映射，就是把数据库中的关系映射到类的对象中。数据库中存储的数据实际上是一种实体与实体之间的关系。而当数据存储到数据库中时，就是持久化的过程。

## jar包(-.-指版本号)

以下是学习中用到的jar包
```swift
1.antlr-.-jar

2.classmate-.-jar

3.dom4j-.-jar

4.hibernate-commons-annotations-.-jar

5.hibernate-core-.-jar

6.hibernate-jpa-.-api-.-jar

7.jandex-.-jar

8.javassist-logging-.-jar

9.jboss-logging-.-jar

10.jboss-transaction-api-.-jar
//操作mysql所需jar包
11.mysql-connector-jar-.-jar
```

## .hbm.xml文件

该文件是用来映射关系与对象（一个pojo类和一个表的映射关系），与需要映射的对象放在同一文件夹下即可，命名方式为：*.hbm.xml，其中*为要映射的类名。

文件头：
```swift
<!DOCTYPE hibernate-mapping PUBLIC 
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
```
在`<hibernate-mapping>`标签中定义关系的`class，table，id，type，property`等属性

## config文件

即hibernate.cfg.xml，该文件放置在class目录/src目录下即可，
```swift
<!-- 当调用Configuration cfg = new Configuration().configure()时，自动搜索本文件，并将其读取到内存中，作为后续操作的基础配置 -->
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
	<!-- 产生操作数据库的session工厂 -->
	<session-factory>
		<!-- 连接数据库的URL -->
		<property name="connection.url">jdbc:mysql://localhost:3306/hiberstudy</property>	
		<!-- 连接数据库的用户名 -->
		<property name="connection.username">root</property>
		<!-- 连接数据库的密码 -->
		<property name="connection.password">123456</property>
		<!-- 连接数据库的驱动类 -->
		<property name="connection.diver_class">com.mysql.jdbc.Driver</property>
		<!-- 数据库方言 -->
		<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
		<!-- 显示hibernate对数据库操作语句 -->
		<property name="hibernate.show_sql">true</property>
		<!-- 自动创建/更新/验证数据库表结构 -->
		<property name="hibernate.hbm2ddl.auto">create</property>
		<!-- 批量操作 -->
		<property name="hibernate.jdbc.batch_size">50</property><!-- 设置批量尺寸 -->
		<property name="hibernate.cache.use_second_level_cache">false</property><!-- 关闭二级缓存 -->
		<property name="hibernate.query.factory_class">
			org.hibernate.hql.ast.ASTQueryTranslatorFactory</property><!-- 设置HQL/SQL查询翻译器属性 更新/删除操作都需要设置 -->
		<!-- 类与表的注册文件，下面是自己在学习过程中的注册文件，-->
		<mapping resource="com/lzf/vo/User.hbm.xml"/>
	</session-factory>
</hibernate-configuration>
```

## 使用过程
```swift
//整个hibernate程序的启动类,如果config配置文件放置在默认路径下，会自动加载不需要带参数
Configuration cfg = new Configuration();
//获得session对象的工厂，保存了对应当前数据库配置的所用映射
SesstionFactory sessionFactory = cfg.configure().buildSessionFactory();
//准备应用session对象来操作数据库，该接口提供了众多持久化方法，如增删改查（非线程安全）
Session session = sessionFactory.openSession();
//事务操作，
Transaction t= session.beginTransaction();
//只有commit之后，才会在数据库中得到更新
t.commit();
```

