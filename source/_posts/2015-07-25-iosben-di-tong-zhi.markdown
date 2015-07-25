---
layout: post
title: "iOS开发 本地通知"
date: 2015-07-25 15:58:22 +0800
comments: true
categories:Blog 
---
iOS开发本地通知，最好的实践就是做一个闹钟程序。这里只说一下我遇到的问题。
###NSLocalNotification
我写了一个闹钟插件，所有的逻辑经检查都没有问题，但就是在测试的时候取消通知总是会取消不完全，比如注册了n个，取消的时候取消n-x个，注册的时候也存在注册数量和自己的预期不一致的情况，反复检查逻辑没有问题。<br>
这里只给出结果，过程不再赘述，原因是线程所致，本地通知的注册与取消在主线程中完成即可避免这个问题。官方文档没有找到合适的解说。可能和UINotification的线程问题同属一类。<br>
关于UINotification，官方是这么描述的：In a multithreaded application, notifications are always delivered in the thread in which the notification was posted, which may not be the same thread in which an observer ...