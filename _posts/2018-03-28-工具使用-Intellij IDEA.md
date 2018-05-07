---
layout:     post
title:      Intellij IDEA
subtitle:
date:       2018-03-28
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - 工具使用
---

# Intellij IDEA遇到的问题

## 1.源发行版和目标版本不对应
Project Structure里确认两个地方:Project sdk以及project language level

Project Structure->Modules里Sources里的Language level

Setting->Build,Execution,Deployment->Compiler->java Compiler->Per-module bytecode Version

## 2:Usage of API documented as @since 1.7+ more... (Ctrl+F1

版本号不对应，修改language版本：

File ->Project Structure->Project Settings -> Modules -> （需要修改的工程名称） -> Sources -> Language Level->选7以上的版本

3