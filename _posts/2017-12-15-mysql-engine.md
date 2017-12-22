MySQL的存储引擎
===========
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