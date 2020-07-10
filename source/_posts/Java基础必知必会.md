---
title: Java基础必知必会
author: 杨鹏
img: https://cdn.jsdelivr.net/gh/zhazhapeng10003/cdn-speed@1.1/medias/featureimages/6.jpg
top: true
cover: false
summary: ' '
toc: true
mathjax: true
comments: true
tags:
  - Java
  - 总结
  categories: 编程基础
abbrlink: 63796
date: 2020-04-02 16:18:36
coverImg:
password:
---


**<font size = 5>基础知识笔记记录，持续更新ing~**  <font size = 3><br>
个人博客：[www.zhazhapeng.cn](https://www.zhazhapeng.cn)<br>

#### 1、JDK\JRE的区别
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** JDK（Java Development Kit）
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;开发工具
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;基本类库
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;javac（编译）
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;javap（反编译）
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;javadoc（编译文档）
&ensp;&ensp;&ensp;&ensp;**<font size = 3 >•** 运行环境（单单运行一个Java程序）
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;JRE（Java Runtime Environment）

#### 2、\== 与 equals 的区别
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** \==：<font color = black>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;基本类型：8种（int\short\long\double\float\byte\boolean\char）；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;引用类型：看引用的对象是否是同一个！
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** equals：<font color = black>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;①重写Object，自己定义比较规则，常见的对象如String等都已经重写了比较的代码；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;②不写，就是比较引用地址是否相同，==

#### 3、HashCode与Equals相同吗
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;[详解](//www.cnblogs.com/keyi/p/7119825.html)

#### 4、Final有什么用
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** Final <font color = black>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;类：不能被继承
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;方法：不能被重写
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;变量：
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;基本类型：值
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;引用类型：引用的对象内部的值可以变

&ensp;&ensp;&ensp;&ensp;类：

```java
final class Father{
}

class Son extends Father{  //Cannot inherit from final '*.Father'
}

```
&ensp;&ensp;&ensp;&ensp;方法：

```java
class Father{
	public final void dosomething(){
		System.out.println(1);
	}
}

class Son extends Father{
	public static void main(String args[]){
		new Son.dosomething();
	}

	public void dosomething(){ //Error:overridden method id final
		System.out.println(2);
	}
}
```
&ensp;&ensp;&ensp;&ensp;变量：

```java
class Father{
	public final void dosomething(){
		System.out.println(1);
	}
}

class Son extends Father{
	private final int a = 10;
	public void setA(int number){
		a = number;    //Error:Cannot assign a value to final variable 'a'
	}
	public static void main(String args[]){
		new Son.dosomething();
	}
}
```
#### 5、操作字符串有哪些类？它们之间有什么区别
&ensp;&ensp;&ensp;&ensp;String：不可变
&ensp;&ensp;&ensp;&ensp;StringBuilder：可变，不加锁，速度快
&ensp;&ensp;&ensp;&ensp;StringBuffer：可变，加锁，线程安全<br/>
#### 6、Java种的 Math.round(-1.5) 等于多少
&ensp;&ensp;&ensp;&ensp;Math.round(-1.5) = -1
>-3, -2, -1, 0, 1, 2
**Math.round()：向右取整**

#### 7、HashMap 与 HashTable 的区别
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** Map：
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;HashMap：线程不安全，速度快，允许放入空值（ HashMap.put(null, null) √ ）；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;HashTable：线程安全，速度慢，不允许放入空值
（多线程的同时执行方法，谁先拿到锁才可以执行，剩下没拿到锁的就等待拿到锁）。
&ensp;&ensp;&ensp;&ensp;<key, value><br/>
#### 8、HashMap
&ensp;&ensp;&ensp;&ensp;[具体详解](//blog.csdn.net/woshimaxiao1/article/details/83661464)<br/>

&ensp;&ensp;&ensp;&ensp;HashMap：
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;存储结构：entry的数组，entry<key, value>，entry本身也是一种链表结构，长度>=8，变成红黑树；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;存储逻辑：根据计算hash值放到对应位置；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;扩容方案：自身容量扩大一倍，成倍增长！<br>
#### 9、Vector 和 ArrayList 的区别
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** List：
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;Vector：上锁，线程安全，速度较慢，增长2×
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;ArrayList：线程不安全，速度较快，增长是1.5×<br/>
&ensp;&ensp;&ensp;&ensp;**<font size = 3>•** Vector为什么用的少：
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;①线程安全，牺牲了速度；
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;②扩容大，需要连续储存空间比较大;
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;③插入、删除比较慢，LinkedList来实现

**<font size = 5>Peace!**