---
layout: post
title:  "智能指针C++实现"
date:   2016-09-02 19:10:00
categories: cpp
tags: cpp
---
看Effective C++书，有关智能指针这一部分，平时项目中也经常遇到，所以在此记录。
智能指针是利用了一种叫做RAII（Resource Acquisition Is Initialization）的技术对普通的指针进行封装，这使得智能指针实质是一个对象，行为表现的却像一个指针。防止用户在new以后忘记delete，还有就是防止在try/catch代码段，程序发生异常，进入catch时候没有释放内存。