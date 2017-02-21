---
layout: post
title:  "智能指针C++实现"
date:   2016-09-02 19:10:00
categories: cpp
tags: cpp
---
看Effective C++书，有关智能指针这一部分，平时项目中也经常遇到，所以在此记录。
智能指针是利用了一种叫做RAII（Resource Acquisition Is Initialization）的技术对普通的指针进行封装，这使得智能指针实质是一个对象，行为表现的却像一个指针。防止用户在new以后忘记delete，还有就是防止在try/catch代码段，程序发生异常，进入catch时候没有释放内存。

智能指针：它的一种通用实现方法是采用引用计数的方法。智能指针将一个计数器与类指向的对象相关联，引用计数跟踪共有多少个类对象共享同一指针。  
-每次创建类的新对象时，初始化指针并将引用计数置为1；  
*当对象作为另一对象的副本而创建时，拷贝构造函数拷贝指针并增加与之相应的引用计数；＊对一个对象进行赋值时，赋值操作符减少左操作数所指对象的引用计数（如果引用计数为减至0，则删除对象），并增加右操作数所指对象的引用计数；这是因此左侧的指针指向了右侧指针所指向的对象，因此右指针所指向的对象的引用计数+1；调用析构函数时，构造函数减少引用计数（如果引用计数减至0，则删除基础对象）。

```C++
template <class T>
class smartpointer
{
private:
	T *_ptr;
public:
	smartpointer(T *p) : _ptr(p)  //构造函数
	{
	}
	T& operator *()        //重载*操作符
	{
		return *_ptr;
	}
	T* operator ->()       //重载->操作符
	{
		return _ptr;
	}
	~smartpointer()        //析构函数
	{
		delete _ptr;
	}
};
```