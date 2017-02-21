---
layout: post
title:  "goahead代码分析"
date:   2016-11-01 20:11:00
categories: cpp
tags: cpp
---
*Web Server*中文名称叫网页服务器或web服务器。WEB服务器也称为WWW(WORLD WIDE WEB)服务器，主要功能是提供网上信息浏览服务。
*GoAhead WebServer*，它是一个源码,免费、功能强大、可以在多个平台运行的嵌入式WebServer。  
由于工作中会用到goahead，所以闲来研究一下。
goahead与前端的交互分为两个接口，*ajax*请求与*表单*提交。