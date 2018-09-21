# 数据库操作

### 创建数据库

~~~mysql
create database 数据库名;
~~~

### 删除数据库

~~~mysql
drop database 数据库名;
~~~

# 表操作

### 创建表

~~~mysql
create table table_name(
    col1 type1 [not null] [primary key],
	col2 type2 [not null]
);

create table tab_new as select * from tab_old [definition only];
~~~

### 删除表

~~~mysql
drop table table_name;
~~~

### 修改表名

```mysql
alter table table1 rename [to] table2;
```

### 字段操作

~~~mysql
# 添加字段
alter table table_name add [column] field1 type;		
# 修改字段名
alter table table1 change field1 field2 type;			
# 修改字段数据类型
alter table table1 modify field1 type;					
# 修改字段位置
alter table table1 modify field1 type first;
alter table table1 modify field1 type after field2;
~~~

### 添加删除主键

~~~mysql
alter table table_name add primary key(col);
alter table table_name drop primary key(col);
~~~

### 创建删除索引

~~~mysql
create [unique] index idxname on table_name(col, ...);
drop index idxname;
~~~

### 创建删除视图

~~~mysql
create view view_name as select ...;
drop view view_name;
~~~

### 表的约束

~~~mysql
primary key			# 主键约束，用于唯一标识对应的记录
foreign key			# 外键约束
not null			# 非空约束
unique				# 唯一性约束
default				# 默认值约束，用于设置字段的默认值
~~~

### 索引

~~~mysql
create table table1(
	id int;
    name varchar(20);
    [索引类型] index index_name(field1)
);
unique				# 唯一索引
fulltext			# 全文索引
spatial				# 空间索引
# 普通 单列 多列
~~~

# 数据操作

### 插入

~~~mysql
insert into table_name(field1, field2) values(value1, value2);
~~~

### 更新

~~~mysql
update table_name set field1=value1 where ...;
~~~

### 删除

~~~mysql
delete from table_name where ...;
~~~

### 查找

~~~mysql
select * from table1 where ...;							# 基本
select * from table1 order by field1, field2 [desc];	# 排序
select count as tablecount from table1;					# 总数
select sum(field) as sumvalue from table1;				# 求和
in like between is
# 分组查询
# 单独使用group by
select * from student group by grade;
# 和聚合函数一起使用
select count(*), grade from student group by grade;
# 和having关键字一起使用
select sum(grade), name from student group by grade having sum(grade) > 100;
~~~

### 操作关联表

~~~mysql
# 交叉连接
select * from student cross join class;
# 内连接
select student.name, class.name from student join class on class.id=student.id;
# 外连接
# 左连接
select * from student left join class on student.id=class.id
# 右连接
select * from student right join class on student.id=class.id
# 子查询
# in
select * from student where cid in (select id from class where id = 2)
# exists，相当于测试，不产生数据，只返回true或false，只有返回true外层才会执行
select * from student where exists(select id from class where id=12);
# any，与比较符一起使用，子查询返回的任一数值都为true，则返回true
# in 等价于 =any
select * from student where cid > any(select id from class);
# all，与比较符一起使用，子查询返回的所有值，如果都为true，则返回true
# not in 等价于 <>any
select * from student where cid > all(select id from class);
~~~

### on与where的区别

在使用left join时，on and 与 on where 条件的区别：

1. on条件是在生成临时表时使用的条件，它不管on中的条件是否为真，都会返回左边表中的记录。
2. where条件是在临时表生成好后，再对临时表进行过滤的条件，这时已没有left join的含义（必须返回左边表的记录）了，条件为真的就全部过滤，on后的条件用于生成左右表关联的临时表，where后的条件对临时表中的记录进行过滤。







