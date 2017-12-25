---
layout: post
title:  "MySQL存储引擎介绍"
date:   2017-12-15 22:21:49
categories: 数据库 
tags: 数据库 
---
MySQL的存储引擎
====
在文件系统中，MySQL会把每个数据库（也叫做架构）保存为数据目录下的一个字目录。当创建一个表时，MySQL会在和表名同名的，以*.frm*为后缀的文件中存储表的定义。  
如果想获知具体每张表使用何种存储引擎，可以用*SHOW TABLE STATUS*命令，下面简述每行输出的意义。    

* Name：表明。
* Engine：表的存储引擎。旧版本为Type，而不是Engine。
* Row_format：行格式，对于MyISAM表，这可能是Dynamic、Fixed或Compressed。动态行的行长度喝表，因为它们包含可变长的字段，例如VARCHAR或BLOG类型字段。固定行，是指行长度相同，由不可变长的字段组成，例如CHAR和INTERGER字段。压缩行只存在于压缩表中。
* Rows：表中的行数，对于非事务性表，这个值是精确的，对于事务表，这通常是估算值。
* Avg_row_length：平均每行包括的字节数。
* Data_length：整个表的数据量（以字节计算）。
* Max_data_length：表可以容纳的最大数据量。
* Index_length：索引数占据磁盘空间的大小。
* Data_free：对于MyISAM表，表示已分配，但现在未被使用的空间。这部分空间包含了以前被删除的行，这些空间可以用于以后的INSERT语句。
* Auto_increment：下一个AUTO_INCREMENT值。
* Create_time：表最初创建时的时间。
* Update_time：表数据最近被更新的时间。
* Check_time：使用CHECK TABLE命令或myisamchk工具检查表时的最近检查时间。
* Collation：指本表中的默认字符集和字符列排序规则（Collation）。
* Checksum：如果启用，则对整个表的内容计算实时的校验和（Checksum）。
* Create_options：指表创建时的其他所有选项。
* Comment：本字段包含了其他额外信息。对于MyISAM表，还包含了注释，如果有注释，将是在表创建时设定的。如果表使用InnoDB存储引擎，将显示InnoDB表空间的剩余空间。如果表是个视图，注释里将包含“VIEW”的文本字样。

MyISAM引擎
----
作为MySQL的默认存储引擎，在性能和可用特征之间，MyISAM提供了一种良好的平衡，这些特征在包括全文检索（Full-Text Indexing）、压缩、空间函数（GIS）。MyISAM不支持事务和行级锁。  
**存储**    
一般来说，MyISAM将每个表存储成两个文件：==数据文件==和==索引文件==。扩展名分别为.MYD和.MYI。MyISAM的格式是平台通用的，这意味着用户可以在不同架构的服务器上毫无问题的互相拷贝数据文件和索引文件。MyISAM表可以包含动态行（Dynamic Row）和静态行（Static Row，即固定长度行）。MySQL会根据表定义决定选用何种行格式。MyISAM表的可容纳的行总数，一般指受限于数据库服务器的可用磁盘空间大小，以及操作系统允许创建的最大文件大小。  
**加锁与并发**  
MyISAM对整张表进行加锁，而不是行。读取程序在需要读取数据时，在所有表上都可以获得共享锁（读锁），而写入程序可以获得排他锁（写锁）。用户在运行select查询时，可以在同一张表内插入新行。  
**自动修复**  
MySQl支持对MyISAM表的自动检查和自动修复。   
**手工修复**    
用户可以使用CHECK TABLE mytable 和 REPAIR TABLE mytable 命令，检查表中的错误，并修复错误。当服务器离线时，也可以使用myisamchk命令行工具检查和修复表。  
**索引特性**。  
在MyISAM表中，用户可以基于BLOB或TEXT类型列的前500个字符，创建相关索引。MyISAM支持全文索引，它可以根据个别单词，为复杂的搜索选项创建相关索引。  
**延迟更新索引（Delayed Key Writes）**
使用表创建选项DELAY_KEY_WRITE创建MyISAM表，在查询结束后，不会将索引的改变数据写入磁盘，而是在内存的键缓冲区（In-memory Key Buffer）中缓存索引改变数据。它只会在清理缓冲区，或者关闭表时，才将索引块转储到磁盘。对于数据经常改变，并且使用频繁的表，这种模式大大提高表的处理性能。
