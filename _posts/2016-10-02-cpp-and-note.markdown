---
layout: post
title:  "C++笔记"
date:   2016-10-01 18:11:00
categories: cpp
tags: cpp
---

记录平时遇到的细节点。  
<h1>sizeof与strlen的区别</h1>
1、sizeof是操作符，strlen是函数；  
2、sizeof操作符的结果类型是size_t，为无符号整型；  
3、sizeof可以用类型做参数，strlen只能用char*做参数，且必须是以"/0"结尾；
4、数组做sizeof参数不退化，传递给strlen就退化为指针了，且在计算字符串数组的长度上有区别；

<h1>#pragma pack的作用</h1>
采用pragma pack可以改变编译器的对齐方式，若不指定，编译器会自动对齐，取编译器对齐方式与自身大小中较小的一个。  

<h1>内联函数使用的场合</h1>
<font color="#FF0000">优点：</font>内联函数的主要目的是，用来替代C语言中表达式形式的宏定义来解决程序中函数调用的效率问题，内联函数代码被放入符号标中，在使用的时候直接进行替换，没有调用的开销，并且内联函数是一个真正的函数，会进行参数类型的检查，并且inline可以作为类的成员函数，可以在使用所在类的保护成员及私有成员。  
<font color="#FF0000">缺点：</font>内联是以代码膨胀（复制）为代价的，仅仅省去了函数调用的开销，从而提高函数的执行效率，如果执行函数体内代码的时间要比函数调用的开销较大，那么效率的收获会很少。并且，每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存。

defaults write com.apple.finder AppleShowAllFiles -bool true

defaults write com.apple.finder AppleShowAllFiles -bool true

