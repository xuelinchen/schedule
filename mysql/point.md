# 索引长度限制
## refer
	http://blog.csdn.net/shaochenshuo/article/details/51064685
## explain
	From the manual at http://dev.mysql.com/doc/refman/5.6/en/create-table.html >>从5.6的官方文档中我们能找到如下双引号中解释  
	"For CHAR, VARCHAR, BINARY, and VARBINARY columns, indexes can be created that use only the leading part of column values, using col_name(length) syntax to specify an index prefix length.  
	...  
	Prefixes can be up to 1000 bytes long (767 bytes for InnoDB tables). Note that prefix limits are measured in bytes, whereas the prefix length in CREATE TABLE statements is interpreted as number of characters ...">>>对于myisam和innodb存储引擎，prefixes的长度限制分别为1000 bytes和767 bytes。注意prefix的单位是bytes，但是建表时我们指定的长度单位是字符。    
	A utf8 character can use up to 3 bytes. Hence you cannot index columns or prefixes of columns longer than 333 (MyISAM) or 255 (InnoDB) utf8 characters.  >>以utf8字符集为例，一个字符占3个bytes。因此在utf8字符集下，对myisam和innodb存储引擎创建索引的单列长度不能超过333个字符和255个字符  

# 修改mysql root密码
## use mysql;update user set password=PASSWORD("C1oudP8x&2017") where user="root";
## flush privileges;
## select Host,User,Password,authentication_string from user;

# insert into ... on duplicate key update ...
## INSERT INTO table (a,b,c) VALUES (1,2,3) ON DUPLICATE KEY UPDATE c=c+1 UPDATE table SET c=c+1 WHERE a=1;