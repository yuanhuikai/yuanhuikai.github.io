---
layout: post
title:  "MySQL点滴记录"
date:   2017-12-22 10:21:49
categories: MySQL 
tags: MySQL 
---
MySQL知识点积累
=====
* SQL 对**大小写**不敏感  
* SQL DML和DDL   
	分为两个部分：数据操作语言(DML)和数据定义语言(DDL)。
	查询和更新指令构成了SQL的DML部分：  
	* SELECT - 从数据库表中获取数据
	* UPDATE - 更新数据库表中的数据
	* DELETE - 从数据库中删除数据
	* INSERT INTO - 向数据库表中插入数据     
	SQL的数据定义语言(DDL)部分使我们有能力创建或删除表哥。我们也可以定义索引(键)，规定表之间的链接，以及施加表间的约束。  
	SQL中最重要的DDL语句如下：  
	* CREATE DATABASES - 创建新数据库
	* ALTER DATABASES - 修改数据库
	* CREATE TABLE - 创建新表
	* ALTER TABLE - 变更（改变）数据库表
	* DROP TABLE - 删除表
	* CREATE INDEX - 创建索引(搜索键)
	* DROP INDEX - 删除索引
* 不同的SQL JOIN类型及它们之间的差异。
	* JOIN：如果表中有至少一个匹配，则返回行。
	* LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行。
	* RIGHT JOIN：即使坐标中没有匹配，也从右表中返回有所得行。
	* FULL JOIN：只要其中一个表存在匹配，就返回行。
* 数据类型(data_type)规定了可容纳何种数据类型。下面的表格包含了SQL中最常用的数据类型：
|数据类型|描述|
|----------------|---------------------------------------|
|integer(size) 
int(size)
smallint(size)
tinyint(size)|仅容纳整数。在括号内规定数字的最大位数|
