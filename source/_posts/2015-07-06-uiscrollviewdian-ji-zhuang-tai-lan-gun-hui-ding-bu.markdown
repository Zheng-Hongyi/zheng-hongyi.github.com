---
layout: post
title: "iOS开发有关界面的那点事儿"
date: 2015-07-06 23:19:50 +0800
comments: true
categories: Blog
---
iOS开发中总会遇到或多或少的坑，这里总结一二。
###UIScrollView那点儿坑
iOS开发，关于UIScrollView点击状态栏回到顶部，这里有个坑，前两天改同事的代码改出来的bug，就是一个界面上只允许有一个UIScrollView允许滚到顶部，若有其他UIScrollView，必须禁掉，否则就都没有了。<br>
进阶：以此类推，所有集成字UIScrollView的视图控件，应该都有这个坑，都要注意。
###有关autolayout
autolayout博大精深，总会有一些实现需要混编，但是有的时候就会有各种意想不到的效果出现，这时候需要考虑一下你用代码写的那一部分UI的autoresizingMask属性，设置为UIViewAutoresizingNone有的时候会帮助你不少忙。
