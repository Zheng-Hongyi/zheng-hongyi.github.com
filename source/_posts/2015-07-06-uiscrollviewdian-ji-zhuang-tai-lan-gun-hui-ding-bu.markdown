---
layout: post
title: "UISCrollView点击状态栏滚回顶部"
date: 2015-07-06 23:19:50 +0800
comments: true
categories: Blog
---
iOS开发，关于UIScrollView点击状态栏回到顶部，这里有个坑，前两天改同事的代码改出来的bug，就是一个界面上只允许有一个UIScrollView允许滚到顶部，若有其他UIScrollView，必须禁掉，否则就都没有了。<br>
进阶：以此类推，所有集成字UIScrollView的视图控件，应该都有这个坑，都要注意