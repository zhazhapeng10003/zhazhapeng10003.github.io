---
title: 对象分配过程TLAB
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed2@1.0/pictures2/reqiqiu.jpg
top: false
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
tags:
  - JVM
  - TLAB
categories: 编程基础
abbrlink: 48440
date: 2020-05-21 16:03:00
coverImg:
password:
---



### 为什么会有TLAB(Thread Local Allocation Buffer)?
&ensp;&ensp;&ensp;&ensp;</font>堆区是线程共享区域，任何线程都可以访问到堆区中的共享数据；<br>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>由于对象实例的创建在JVM中十分频繁，一次在并发环境下从堆区中划分内存空间是线程不安全的<br>&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>为避免多个线程操作同一地址，需要使用加锁等机制，进而影响分配速度。

### 什么是TLAB?
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>从内存模型而不是垃圾收集的角度，对Eden区域继续进行划分，JVM为<font color=red>每个线程分配了一个私有缓存区域</font>，它包含在Eden区域内。<br>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>多线程同时分配内存时，使用TLAB可以避免一系列的非线程安全问题，同时还能够提升内存分配的吞吐量，因此我们可以讲这种内存分配方式成为<font color=red>快速分配策略</font><br>
### TLAB的再说明：
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>尽管不是所有的对象实例都能够在TLAB中成功分配内存，但<font color=red>JVM确实是将TLAB作为内存分配的首选。</font><br>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>在程序中，开发人员可以通过选项“-XX:UseTLAB”设置是否开启TLAB空间。<br>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>默认情况下，TLAB空间的内存非常小，<font color=red>仅占有整个Eden空间的1%</font>，当然我们可以通过选项“-XX:TLABWasteTargetPercent”设置TLAB空间所占用Eden空间的百分比大小。<br>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** </font>一旦对象在LAB空间分配内存失败时，JVM就会尝试着通过使用加锁机制确保数据操作的原子性，从而直接在Eden空间中分配内存。<br>
![](https://img-blog.csdnimg.cn/20200520140531526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYwODY0NQ==,size_16,color_FFFFFF,t_70)
<font size = 5>**Peace!💪**
