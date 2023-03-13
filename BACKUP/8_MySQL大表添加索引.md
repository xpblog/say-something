# [MySQL大表添加索引](https://github.com/xpblog/say-something/issues/8)

[返回目录](https://github.com/xpblog/say-something)

## 大表为什么不直接加索引
MySQL添加索引会锁表，所以如果给数据量大的表添加索引，就会出现锁表。

## 解决方案一
无锁加索引，ALGORITHM 和 LOCK 参数在 MySQL 中是从 5.6 版本开始引入的（因此如果是5.6之前的版本就不能用这种方式了）。
```sql
table table_name add index index_name (column_name) ALGORITHM=INPLACE, LOCK=NONE;
```
**ALGORITHM(译:算法)：**
- DEFAULT：表示让 MySQL 自行选择算法。
- COPY：表示创建一个新表，将原表的数据复制到新表中，然后重命名新表。这个过程需要较长的时间，并且需要使用表锁定。
- INPLACE：表示在不复制整个表的情况下，只修改表的结构。这可以减少锁定的时间，从而减少对系统性能的影响。

**LOCK：**
- DEFAULT：表示让 MySQL 自行选择锁定类型。
- NONE：表示不进行锁定。
- SHARED：表示对表进行共享锁定，以允许其他读取操作并发进行，但阻止写入操作。
- EXCLUSIVE：表示对表进行排他锁定，以阻止其他所有操作。这个锁定级别通常用于修改表结构或执行大批量插入操作。

## 解决方案二
一、先创建一张跟原表A数据结构相同的新表B
```sql
create table B like A;
```
二、在新表B添加需要加上的新索引

三、把原表A数据导到新表B，导入前可以把B表的非主键索引删掉，增加导入效率。数据量大也可以分批导入
```sql
alter B drop index 索引名;

insert into B select * from A limit 0,1000;
```
四、新表B更名为表名A，原表A换别的表名

**注：如果在加索引的过程中出现的数据增删改，会有数据不一致的情况**
