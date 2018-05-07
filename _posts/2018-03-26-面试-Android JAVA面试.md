---
layout:     post
title:      Android JAVA面试
subtitle:
date:       2018-03-26
author:     Felix
header-img: img/home-bg-art.jpg
catalog: true
tags:
    - 面试
---
# 一、Android面试：

## 1.Android6.0新特性，

1）动态权限申请

动态权限需要在软件运行时单独申请，目前有9组：
CONTACTS、PHONE、CALENDAR、CAMERA、SENSORS、LOCATIONS、STORAGE、MICROPHONE、SMS

普通权限正常在Androidmanifest.xml文件中申请即可。

注：如果targetSDKVersion设置为23，则必须按照Android谷歌的要求动态申请权限，如果暂时不打算支持动态权限，则targetSDKversion最大只能设置为22.

申请步骤：

检查是否有此权限checkSelfPermission（）；
如果有，直接做接下来的步骤，如果没有，解释给用户为何要申请，shouldShowRequestPermissionRationale；
如果需要返回true，如果不需要，返回false，

2）新特性2：APPLink，比如在邮箱里点击一个微博连接，如果手机中有微博APP，则会跳转到该APP。

## 2.activity生命周期

1）常见状态：

onCreate——onStart——onResume——onPause——onStop——onDestroy；

该状态是一个activity从创建到销毁的过程，当对activity执行其他操作时activity还有其他的状态：

当按手机的home键时，activity不可见，但此时并未销毁activity，而是进入了onStop状态，此时，如果再进入该应用，会重启（onRestart）activity，然后进入onStart状态。

onPause和onResume，假如该页面上有个对话框，此时是不能操作activity的，且处于onPause位置，当对话框消失，也就进入了onResume页面。

切换横竖屏的时候会先执行onSaveInstanceState()，再执行生命周期，切回去的时候 会执行onRestoreInstanceState()；当切换屏幕时，在save中不做其他操作的话，会造成数据丢失。

Fragment较activity多了绑定activity和解绑的过程，以及当销毁fragment时，销毁先销毁fragment的View对象，再销毁fragment

## 3.四种启动模式

1）standard（默认）：

每次启动activity都会创建一个activity；

2）singleTop：

启动activity时，会判断是否存在于栈顶，如果在直接复用，否则创建新的实例；

3）singleTask：

从栈中检查是否有activity，有的话将其他activity出栈，直到目标activity；

4）singleInstance：

指定为singleInstance的activity会启动一个新的栈来管理activity实例，但是无论是哪个任务栈中，该实例在系统中都只有一个。典型的singleInstance：来电界面；

## 4.Service

1）减少ANR错误，用于执行耗时操作，

2）两种启动方式：

startService：后台长期运行，直到资源不足，当有资源时，又会重启

bindService：与调用者绑定，调用者退出，service也会退出，可以调用服务内部方法

常用混合开启模式：start()-bind()-unbind()-stop();即可以长期运行，又可以使用服务内部方法，也就是说，主要区别在于是否能够使用内部方法，以及是否可以长期执行，这两点都是服务的优点。

## 5.Android异步消息处理

1）Handler方式
创建一个Handler，并重写handlerMessage()方法，当子线程中需要进行UI操作时，创建一个Message对象，并通过Handler发送出去，发出去的消息会进入MessageQueue，Looper()会一直尝试从MessageQueue中取消息，最后分发给handlerMessage，由于Handler是在主线程中创建的，因此handlerMessage也是在主线程中运行，这样就可以保证安全地进行UI操作了；
实质上是同一个进程的线程间通信，Android系统中，其实都是运行在Android所fork的进程上，除非再新添加其他进程
2）AsyncTask其实是对Handler的封装，

## 6.广播

哪些消息可以是广播：手机开机、电量、时间或时区、网络变化等；

1）无序（标准）广播：不可拦截

2）有序广播：可拦截，同一时刻只有一个广播接收器能收到这条广播，广播接收器的优先级决定该广播接收的位置。

静态注册：Androidmanifest.xml文件中注册；例：可以在手机开机之后就接收到开机广播

动态注册：调用registerReceiver()方法，动态注册之后一定要取消注册，防止内存泄露。缺点：但是必须在程序启动后才能使用，因为是注册在onCreate中的。

## 7.ContentProvider

共享数据，实际上是对数据的操作，包括CRUD操作，

## 8.Android中操作Excel的jar包：jxl.jar

主要包括jxl（读文件）、jxl.format、jxl.write（写文件）；

## 9.Android事件分发机制

activity——ViewGroup——View（实际上是页面的组成，activity由各种ViewGroup组成，ViewGroup由许多单个View组成）

从左到右执行，关联的方法为：dispatchTouchEvent()，onInterceptTouchEvent()，onTouchEvent();
当onInterceptTouchEvent()拦截到事件后，若返回true，就会交给onTouchEvent()执行，否则交给子View处理

## 10.OOM异常（内存溢出）

主要由图片过多过大引起的————（解决）调整图片大小，如缩放；及时回收不用的图片资源。

## 11.内存泄露

垃圾没有及时回收，就会造成内存泄露了
虽然有自动回收机制，但是不代表完全可以忽略分配，或忽略释放内存；

## 12.ANR异常

5秒：按键或触摸时间在指定的时间内无响应————避免耗时操作，如网络，操作数据库，处理大文件等
10秒：广播接收器在指定时间内无法处理完成————避免耗时操作
20秒：service在指定时间内无法完成（小概率事件）————避免同步死锁等

可以在可能出现耗时操作的地方添加progress进度条，提醒用户进度。

布局也要优化，避免多层嵌套；嵌入过多会造成java.lang.StackOverflowError（堆栈溢出错误）的错误，为了兼容低版本手机，保证在5层及以下，如果不是兼容低版本手机，也最好不要超过10层，避免出现堆栈溢出错误。

## 13.JNI

native方法会告诉编译器该方法是本地语言，Java可以直接拿来用。

## 14.OkHttp

Android Studio中使用OKhttp时，在gradle中添加compile 'com.squareup.okhttp:版本号'
与此同时，还要导入okio包；

在eclipse中导入的话，添加jar包。

# 二、Java面试

## 1.序列化和反序列化

通过实现序列化接口：Serializable，在Java中使用对象流来完成序列化和反序列化
output：序列化（写操作）：把Java对象数据通过某种方式存储到磁盘文件或传递给其他网络节点上。
input：反序列化（读操作）：把磁盘文件或网络节点上的对象数据恢复成Java对象模型的过程。

## 2.四种引用方式：

强引用：垃圾回收器不会回收它；

弱引用：具有短暂的生命周期，不管是否有空间都会回收，但是GC线程优先级低，所以不一定回马上回收；

软引用：如果内存空间够，就不会回收，内存空间不够才会回收；

虚引用：任何时候都可以被回收

## 3.浅复制和深复制

浅复制只是copy了地址，也就是说，当地址中的属性、值等改变之后，复制的对象也会改变；

而深复制，不仅将原对象的各个属性复制出去，而且将原对象各个属性所包含的对象也依次采用深复制的方法复制到新对象上，那么此时也就不是指向同一个对象了，

## 4.map转换成set操作

map是键值对的存储形式，set继承自collection，有iterator迭代器，所以可以通过keySet()方法，或者entrySet()方法来访问map，使用迭代器取出map集合中的元素。

## 5.switch case

在Java7中开始支持String类型，但实质上还是int类型的对比，因为String对象调用hashcode之后，生成int类型的hash值，最终是用hash值来匹配所有的case；

## 6.object中的方法

构造方法：object()
native方法：registerNatives();
clone()
getClass()
equals()
hashcode()
toString()
wait()/notify()/notifyAll()
finalize()

## 7.组合和继承

组合是显式的：组合实际上就是使用已有的类，显式地创建类对应的对象

继承是隐式的：直接继承对象

## 8.hashmap

哈希表，实际上就是数组和链表的结合；

hashmap键值对的存储方式，可以存储null值，当两个对象的hashcode相同时，如果要获取数据，会先通过hashcode获取链表，再通过equals获取对应节点上的值，

负载因子为0.75，也就是说当存储到75%时，Rehashing，即再散列

## 9.泛型

K：key
V: value
T: Type
E: enum
?: 通配符,表示不确定

## 10.重写与重载

重载只与参数列表有关

重写必须与被重写的方法名相同

## 11.依赖注入

将对象保存在XML中，这样，要修改或者添加对象的时候  只需要改动XML文件就可以了。

