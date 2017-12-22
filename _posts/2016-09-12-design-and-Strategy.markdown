---
layout: post
title:  "策略模式"
date:   2016-09-12 19:10:00
categories: 设计模式
tags: 设计模式
---
目前在看《Head First设计模式》这本书，书中的代码都是以Java实现，在此以C++代码实现，加深理解。   
策略模式：定义了算法族，分别封装起来，让它们之间可以相互替换，此模式让算法的变化独立于使用算法的客户。 
OO原则：封装变化、多用组合，少用继承、针对接口编程，不针对实现编程。  
<div align="center">
	<img src="/assets/plantuml/Strategy-design.png" height="400" width="200" align="center">
</div>
``` c++
class SayBehavior {  
public:       
        void virtual Say() = 0;   
    }; 

class ChinaSay : public SayBehavior {
public:
    void Say(){
        cout << "你好" << endl;
    }
};

class EnglishSay : public SayBehavior {
public:
    void Say(){
        cout << "Hello" << endl;
    }
};

class Persion {
public:
    Persion():m_SayBehavior(0){}
    void SetSayBehavior(SayBehavior *lrs){
        this->m_SayBehavior = lrs;
    }
    void virtual Speak();
protected:
    SayBehavior *m_SayBehavior;
};

class Chinease : public Persion{
public:
    void Speak() {
        m_SayBehavior->Say();
    }
};

int main(int argc, const char * argv[]) {

    ChinaSay *chinaSay = new ChinaSay();
    EnglishSay *englishSay = new EnglishSay();
    
    Persion *chinaPer = new Chinease();
    chinaPer->Speak();
        
    chinaPer->SetSayBehavior(chinaSay);
    chinaPer->Speak();
          
    chinaPer->SetSayBehavior(englishSay);
    chinaPer->Speak();
    
return 0;
}
```
