---
layout:     post
title:      ssh key连接多个github账号
subtitle:
date:       2017-10-20
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - ssh key
    - github
---

## 一、单账号

当我们想在本地push代码带远程仓库，每次在执行pull 或者push操作时，都会提示输入用户名密码，为了避免重复输入密码，则要使用ssh-keygen命令添加ssh key
这样的每次pull 或者push的时候，都不会重复输入用户名密码。
基本的添加ssh key的方法为：
```swift
ssh-keygen -t rsa -C "email" (操作结束会生成一个rsa文件)
-> Enter file in which to save the key (~/.ssh/id_rsa):  该语句提示我们输入生成的key文件的名称，括号里面是该秘钥的路径
ssh-add ~/.ssh/id_rsa   即将私钥添加到ssh中
```
然后在对应的路径下找到id_rsa.pub,用记事本打开即可，复制到github的setting->SSH and GPG keys中

即可以使用git的方式clone pull 以及push到远程，与远程操作

## 二、多账号

如果利用步骤一中的操作，那么重新生成的key会跟第一个混淆，或者可以说会覆盖掉第一次生成的key
此时，需要知道如何才能生成第二个key：

1.先清除一些global user.name  user.email,或者重新设置一次，覆盖掉之前的name, email
    `git config --global --unset user.name`（可以清除用户名，清除email方式类似）
2.`ssh-keygen -t rsa -C "email"`
`Enter file in which to save the key (~/.ssh/id_rsa):id_rsa_new`    此时会在当前操作路径下生成一个名为id_rsa_new的key
`ssh-add ~/.ssh/id_rsa_new`
如果出现`Could not open a connection to your authentication agent`的错误，
尝试使用`ssh-agent bash`
然后再用`ssh-add ~/.ssh/id_rsa_new`将新的密钥添加到ssh中

在第二个账号中添加key的方法与步骤一相同

3.重点：
如何区分两个密钥，
此时需要在~/.ssh文件夹下创建config
如果有不需要创建，没有的话执行
    `touch config`

config中的内容编辑如下：
```swift
# 该文件用于配置私钥对应的服务器
# Default github user(1161093241@qq.com)
Host github.com   #Host就是每个SSH连接的单独代号，identityFile告诉连接去读取哪个私钥
 HostName github.com
 User git
 IdentityFile C:/Users/Hasee/.ssh/id_rsa

 # second user(2223505357@qq.com)
 # 建一个github别名，新建的帐号使用这个别名做克隆和更新
Host github2
 HostName github.com
 User git
 IdentityFile C:/Users/Hasee/.ssh/id_rsa_m
```
## 应用举例：

1.测试是否配好私钥
```swift
ssh -T git@github.com(默认key)
ssh -t github2(自己创建的key对应的host)
```
2.clone举例:
```swift
git clone github2:账号名/仓库名.git
```
## 缺点：
目前我感觉缺点是，在自己想要操作的仓库下操作之前，要先用git config 覆盖一次账号 邮箱，否则提交代码的用户是会有交叉提交的现象。
当然还是比每次pull  push 的时候要填写用户名密码好多了，毕竟每次操作只需要修改一次

## 感谢博主：

[http://www.jianshu.com/p/89cb26e5c3e8](http://www.jianshu.com/p/89cb26e5c3e8)

[https://my.oschina.net/csensix/blog/184434](https://my.oschina.net/csensix/blog/184434)

[http://www.cnblogs.com/BeginMan/p/3548139.html](http://www.cnblogs.com/BeginMan/p/3548139.html)


