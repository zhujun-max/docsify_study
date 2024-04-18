**重要事项**
+ 一定要记住，SQL 对大小写不敏感！
+ 某些数据库系统要求在每条 SQL 命令的末端使用分号。

### SQL DML和DDL
可以把sql语句分为两个部分：
SELECT LastName FROM Persons
数据库操作语言（DML）和数据定义语言（DDL）

查询和更新指令构成了SQL的DML部分：
+ SELECT -从数据库表中获取数据
+ UPDATE -更新数据库表中的数据
+ DELETE -从数据库中删除数据
+ INSERT INTO -向数据库中插入数据

SQL的数据定义语言（DDL）部分使我们有能力创建或删除表格。

+ CREATE DATABASE -创建新数据库
+ ALTER DATABASE -修改数据库
+ CREATE TABLE -创建新表
+ ALTER TABLE -变更（改变）数据库表
+ DROP TABLE -删除表
+ CREATE INDEX -创建索引（搜索键）
+ DROP INDEX -删除索引