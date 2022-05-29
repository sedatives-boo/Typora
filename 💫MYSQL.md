### 基本操作

```sql
show database;
```

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| db1                |
| mysql              |    （用于描述用户权限）
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.02 sec)
```

```sql
create database db_name;
drop database db_name;
```

 查看搜索引擎

```sql
show engines;
```

```
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```

其中support 表示引擎能否使用，Default表示当前默认引擎。

选定当前数据库

```sql
use zoo;
```

查看数据库信息

```sql
show create database zoo;
```

## 数据表

数据表是数据存储的基本单位。数据表被定义为列的集合。

每行代表一个记录，每列代表记录的一个域。

#### 创建表

```sql
create table <表名>
(
字段名1，数据类型[列级别约束条件][默认值]，
字段名2，数据类型[列级别约束条件][默认值]，
);
```

示例

```sql
use zoo;
mysql> create table animals/*创建时没有设置主键之后不能更改*/
    -> (id int(10),
    -> name varchar(10)
    -> );
Query OK, 0 rows affected (0.05 sec)/*注意括号里要填精度*/
```

设置主键：

1. 在创建表时同时设置    id int(10) primray key,
2. 定义完所有列后设置    primary key (id,name));  该方法使用多字段主键

外键：

一个表有一个或多个外键，外键对应**参照完整性**。

外键一定对应另一个表的主键

```sql
constraint 外键名 foreign key(字段名) references 主表名(主键)
```

非空约束：

```sql
name varchar(10) not null,
```

唯一性约束：

```sql
name varchar(22) unique,
```

默认约束：

```sql
deptId int(11) default 11,
```

**属性自动增加**

在每次增加新记录时，自动生成主键值：

`auto_increment`

初始值是1，且一个表只有一个字段才能使用，且必须是主键的一部分，适用任何整数类型（`tinyint`,`smallint`,`int`,`bigint`）

```sql
id int(11) primary key auto_increment,
```

#### 查看结构

```sql
/*插入语句*/
insert into animals(name,weight)
 value('Lion',200),('fish',100),('Tiger',180);
/*打印所有条目*/
select * from animals;
/*描述表*/
desc animals;
/*查看表的创建信息*/
show create table animals;
show create table animals\G;/*显示会简洁些*/
```

实例

```sql
mysql> create table animals;
ERROR 1113 (42000): A table must have at least 1 column
mysql> create table animals(
    -> id int(10) primary key auto_increment,
    -> name varchar(10) not null,
    -> weight float
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> insert into animals(name,weight)
    -> value('Lion',200),('fish',100),('Tiger',180);
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from animals;
+----+-------+--------+
| id | name  | weight |
+----+-------+--------+
|  1 | Lion  |    200 |
|  2 | fish  |    100 |
|  3 | Tiger |    180 |
+----+-------+--------+
3 rows in set (0.00 sec)

mysql> desc animals;
+--------+-------------+------+-----+---------+----------------+
| Field  | Type        | Null | Key | Default | Extra          |
+--------+-------------+------+-----+---------+----------------+
| id     | int(10)     | NO   | PRI | NULL    | auto_increment |
| name   | varchar(10) | NO   |     | NULL    |                |
| weight | float       | YES  |     | NULL    |                |
+--------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

mysql> show create table animals;
+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table   | Create Table                                                                                                                                                                                                |
+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| animals | CREATE TABLE `animals` (
  `id` int(10) NOT NULL AUTO_INCREMENT,
  `name` varchar(10) NOT NULL,
  `weight` float DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=latin1 |
+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

这里注意到字符集为拉丁



#### 修改数据表

修改表名

```sql
/* [] 表示可以省略*/
alter table <旧表名> rename [to] <新表名>;
```

修改字段数据类型

```sql
alter table <表名> modify <字段名><数据类型>;
```

修改字段名

```sql
alter table <表名> change <旧字段名><新字段名><新数据类型>;
```

添加字段

```sql
alter table <表名> add <新字段名> <数据类型>
[约束条件] [first|after 已存在字段名]
/*first 表示新字段作为表的第一个字段，after 表示插入制定字段后面*/
```

删除字段

```sql
alter table <表名> drop <字段名>;
```

修改字段的排列位置

```sql
alter table <表名> modify <字段名1><数据类型> first |after<字段名2>;
```

更改表的存储引擎

```sql
alter table <表名> engine=<更改后的引擎>;
```

删除表的外键约束

```sql
alter table <表名> drop foreign key <外键名>;
```

#### 删除数据表

```sql
drop table [if exists] 表1,表2...;
/*if exists 即使表不存在也不会报错，但会警告*/
```

如果存在外键关联，则直接删除父表会显示失败，破坏了**参照完整性**，做法两种：

1. 先删除子表再删除父表；
2. 删除外键约束再删除父表

## 5.数据类型和运算符

整数类型

| 类型      | 存储  | 有符号范围   | 无符号范围 |
| --------- | ----- | ------------ | ---------- |
| tinyINT   | 1字节 | -128~127     | 0~255      |
| smallINT  | 2字节 | -32768~32767 | 0~65535    |
| mediumINT | 3字节 |              |            |
| INT       | 4字节 |              |            |
| bigINT    | 8字节 |              |            |

MySQL采用浮点和定点数表示小数，可以用（M，N）表示，M为精度，N为标度，表示小数的位数

| 类型                 | 说明                  | 存储需求 |
| -------------------- | --------------------- | -------- |
| FLOAT                | 单精度                | 4字节    |
| DOUBLE               | 双精度                | 8字节    |
| DECIMAL（M，D），DEC | 压缩的“严格” 的定点数 | M+2字节  |

创建表指定小数类型：

```sql
create table temp (x float(5,1),  y double(5,1),  z decimal(5,1));
```

插入数据

```sql
insert into temp values(5.12, 5.15, 5.123);
/*会得到警告，通过打印警告：*/
show warnings;
/*告知z会被截断*/
```

查看数据

```sql
select * from temp;
/*x， y， z分别为5.1， 5.2， 5.1*/
```

浮点数和定点数在长度一定时，浮点数能显示更大的数据范围，但会有精度问题。注意避免用浮点数做计算比较。

在MySQL中，定点数以**字符串形式**存储。

### 日期和时间

| 类型      | 格式                         | 存储需求 |
| --------- | ---------------------------- | -------- |
| YAER      | YYYY（输入2022，或者'2022'） | 1字节    |
| TIME      | HH:MM:SS                     | 3字节    |
| DATE      | YYYY-MM-DD或者YY-MM-DD       | 3字节    |
| DATETIME  | YYYY-MM-DD HH:MM:SS          | 8字节    |
| TIMESTAMP | YYYY-MM-DD HH:MM:SS          | 4字节    |

使用/   .   @   代替 - 符号都是可以的 

```sql
mysql> insert into tmp values('10:05:05'),('23:23'),('2 10:10'),('23');
Query OK, 4 rows affected (0.02 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select * from tmp;
+----------+
| t        |
+----------+
| 10:05:05 |
| 23:23:00 |
| 58:10:00 |
| 00:00:23 |
+----------+
4 rows in set (0.00 sec)
```

如果没有冒号，就会假定最后两位为秒，如'1112'表示00:11:12，如果使用冒号就表示当天的时间'11:22'表示11:22:00

**date**

```sql
mysql> insert into tmp5 values('1988-08-08'),('19990202'),(211212);
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from tmp5;
+------------+
| d          |
+------------+
| 1988-08-08 |
| 1999-02-02 |
| 2021-12-12 |
+------------+
3 rows in set (0.00 sec)
```

使用系统函数插入日期

```sql
mysql> insert into tmp5 values (current_date()), (now());
Query OK, 2 rows affected, 1 warning (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 1

mysql> select * from tmp5;
+------------+
| d          |
+------------+
| 2022-03-26 |
| 2022-03-26 |
+------------+
2 rows in set (0.00 sec)
```

**TIMESTAMP**

TIMESTAMP和DATETIME相同显示宽度在19个字符，TIMESTAMP根据UTC存储

```sql
/*设置时区*/
set time_zone = '+10:00';
```

### 文本字符串类型

除了可以存储字符串类型，还能存储图片和声音等二进制数据。MySQL支持两种字符型数据：

- 文本字符串
- 二进制字符串

MySQL的文本字符串有：

| CHAR | VARCHAR | TEXT | ENUM | SET  |
| ---- | ------- | ---- | ---- | ---- |

**CHAR和VARCHAR**

char是定长，varchar是变长类型，char的处理速度更快，但浪费存储空间

> 注意书P105的MyISAM和InnoDB的区别

对于char(4)只能存储4字节的字符串，char最多可定义char(255)

Varchar(4)根据字符串长度调整存储空间，实际为L+1（其中1 字节存储字符串长度），当字符串长度为5时，为6，而显示为4字节。

```sql
mysql> create table tmp8(
    -> ch char(4), vch varchar(4)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> insert into tmp8 values('ab  ','ab  ');
Query OK, 1 row affected (0.01 sec)

mysql> select * from tmp8;
+------+------+
| ch   | vch  |
+------+------+
| ab   | ab   |
+------+------+
1 row in set (0.00 sec)

mysql> select concat('(',ch, ')'),concat('(',vch,')') from tmp8;
+---------------------+---------------------+
| concat('(',ch, ')') | concat('(',vch,')') |
+---------------------+---------------------+
| (ab)                | (ab  )              |
+---------------------+---------------------+
1 row in set (0.01 sec)
/*注意这里用concat函数将字符的空格显示出来*/
```

**TEXT类型**

保存非二进制字符串，如文章内容，评论。不删除尾部空格

Text分为四种：Tinytext,text,Mediumtext,Longtext.

**ENUM类型**

ENUM是一个字符串对象，语法格式为：

```sql
字段名 ENUM('值1','值2',...,'值n')
```

```sql
mysql> create table tmp10(soc int,level enum('excellent','good','bad'));
Query OK, 0 rows affected (0.04 sec)

mysql> insert into tmp10 values(70,'good'),(90,1),(75,2),(50,3);/*可根据编号存储*/
Query OK, 4 rows affected (0.02 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> insert into tmp10 values(100,'best');/*ENUM没有的值不能插入*/
ERROR 1265 (01000): Data truncated for column 'level' at row 1
mysql> select * from tmp10;
+------+-----------+
| soc  | level     |
+------+-----------+
|   70 | good      |
|   90 | excellent |
|   75 | good      |
|   50 | bad       |
+------+-----------+
4 rows in set (0.00 sec)
```

**SET类型**

set是一个字符串对象，可以有零个或多个值，set列最多有64个成员

与ENUM不同，SET可以定义的列值选多个字符的联合。

```sql
mysql> create table tmp11(a set('a','b','c','d'));
Query OK, 0 rows affected (0.03 sec)

mysql> insert into tmp11 values ('a'),('a,b,a');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from tmp11;
+------+
| a    |
+------+
| a    |
| a,b  |
+------+
2 rows in set (0.00 sec)
```

### 二进制字符串类型

| 类型          | 说明       | 存储需求        |
| ------------- | ---------- | --------------- |
| BIT(M)        | 位字段类型 | 大约(M+7)/8字节 |
| BINARY(M)     | 固定长度   | M字节           |
| VARBINARY(M)  | 可变长度   | M+1字节         |
| TINYBLOB(M)   |            | L+1字节         |
| BLOB(M)       |            | L+2字节         |
| MEDIUMBLOB(M) |            | L+3字节         |
| LONGBLOG(M)   |            | L+4字节         |

**BIT类型**

大于’1111‘的二进制无法被插入到BIT(4)中，即最大为15

```sql
mysql> create table tmp12( b bit(4));
Query OK, 0 rows affected (0.02 sec)

mysql> insert into tmp12 values(2),(9),(15);
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select bin(b+0) from tmp12;/*b+0表示将二进制结果转化位对应值，BIN（）函数将数字转化为二进制*/
+----------+
| bin(b+0) |
+----------+
| 10       |
| 1001     |
| 1111     |
+----------+
3 rows in set (0.02 sec)
```

**BINARY和VARBINARY**

```sql
mysql> create table tmp13(
    -> b binary(3), vb varbinary(30)
    -> );
Query OK, 0 rows affected (0.02 sec)

mysql> insert into tmp13 values(5,5);
Query OK, 1 row affected (0.00 sec)
/*查看字段存储数据长度*/
mysql> select length(b), length(vb) from tmp13;
+-----------+------------+
| length(b) | length(vb) |
+-----------+------------+
|         3 |          1 |
+-----------+------------+
1 row in set (0.02 sec)

/*进一步确认 5 的存储方式*/
mysql> select b, vb, b='5' ,b='5\0\0',vb='5',vb='5\0\0' from tmp13;
+------+------+-------+-----------+--------+------------+
| b    | vb   | b='5' | b='5\0\0' | vb='5' | vb='5\0\0' |
+------+------+-------+-----------+--------+------------+
| 5    | 5    |     0 |         1 |      1 |          0 |
+------+------+-------+-----------+--------+------------+
1 row in set (0.01 sec)
/*看出b填充了0，而变长字段没有填充*/
```

**BLOB类型**

BLOB是一个二进制大对象，用来存储可变数量的数据。BLOB存储图片、音频信息，而Text存储纯文本

### 运算符

算术运算符

```sql
select least('a','b','c');
select greatest(1,2,3);
select 2 in (1,2,3,4);/*返回0，1*/
```

`LIKE` 用于字符串匹配

> 通配符
>
>  %   匹配任何数目的字符，包括零字符
>
> _ 只能匹配一个字符

```sql
select 'stud' like 'stud','stud' like 'stu_','stud' like 'st%';
```

`REGEXP`用于匹配字符串

```sql
expr regexp 条件1
/*如果expe满足条件，返回1 否则返回0*/
```

> 通配符
>
> ^	匹配以该字符后面的字符开头的字符串
>
> $  匹配以该字符后面的字符结尾的字符串
>
> .    匹配任何一个单字符
>
> [...]  匹配在方括号内的任何字符，如[a,b,c]，也可以用-，如[a-z]表示所有 
>
> /*  匹配零个或多个在它面前的字符，例如"x*"匹配任意数量的x字符，"[0-9]**"匹配任意数量的数字（一个星号）

```sql
select 'ssky' regexp '^s','ssky' regexp'y$','ssky' regexp '.sky','ssky' regexp '[ab]';

+--------------------+-------------------+----------------------+----------------------+
| 'ssky' regexp '^s' | 'ssky' regexp'y$' | 'ssky' regexp '.sky' | 'ssky' regexp '[ab]' |
+--------------------+-------------------+----------------------+----------------------+
|                  1 |                 1 |                    1 |                    0 |
+--------------------+-------------------+----------------------+----------------------+
1 row in set (0.00 sec)
/* ^s 匹配以s开头的字符串
  $y 匹配以y结尾的
  .sky 匹配任意单字符
  [ab] 匹配任意包含a或b的字符串*/
```

逻辑运算符

## 6.MySQL函数

随机数

> rand()，返回0~1.0之间
>
> rand(x)，当里面参数（整数）相同时，值相等

```sql
mysql> show processlist;
+----+------+-----------------+---------+---------+------+----------+------------------+
| Id | User | Host            | db      | Command | Time | State    | Info             |
+----+------+-----------------+---------+---------+------+----------+------------------+
|  2 | root | localhost:57210 | company | Sleep   |   67 |          | NULL             |
|  3 | root | localhost:57274 | NULL    | Query   |    0 | starting | show processlist |
+----+------+-----------------+---------+---------+------+----------+------------------+
2 rows in set (0.01 sec)

mysql> kill 2;
Query OK, 0 rows affected (0.01 sec)

mysql> show processlist;
+----+------+-----------------+------+---------+------+----------+------------------+
| Id | User | Host            | db   | Command | Time | State    | Info             |
+----+------+-----------------+------+---------+------+----------+------------------+
|  3 | root | localhost:57274 | NULL | Query   |    0 | starting | show processlist |
+----+------+-----------------+------+---------+------+----------+------------------+
1 row in set (0.00 sec)
```

### 加密解密函数

使用password函数，注意只能在服务器的鉴定系统中使用，不应在个人程序中使用，该过程是单向的

```sql
mysql> select password('zhuzhu12321');
+-------------------------------------------+
| password('zhuzhu12321')                   |
+-------------------------------------------+
| *6614D940A7E711F025AD71A2B170DBCC8B4B20FD |
+-------------------------------------------+
1 row in set, 1 warning (0.00 sec)
```

#### MD5(str)

#### ENCODE(ste,pswd_str)

Encode 和 Decode 互逆，encode生成二进制乱码（但是长度和原密码长度相同）

```sql
mysql> select encode('popzhu','cry');
+------------------------+
| encode('popzhu','cry') |
+------------------------+
| 义+ß.ï                 |
+------------------------+
1 row in set, 1 warning (0.01 sec)

mysql> select decode(encode('popzhu','cry'),'cry');#使用同样的字符串解密，得出结果相同
+--------------------------------------+
| decode(encode('popzhu','cry'),'cry') |
+--------------------------------------+
| popzhu                               |
+--------------------------------------+
1 row in set, 2 warnings (0.00 sec)
```

### 格式化函数

使用 `format(x,n)` 函数保留小数点后n位

```sql
mysql> select format(1234.32234,2),format(0.001,5);
+----------------------+-----------------+
| format(1234.32234,2) | format(0.001,5) |
+----------------------+-----------------+
| 1,234.32             | 0.00100         |
+----------------------+-----------------+
1 row in set (0.00 sec)
```

### 进制转换

`conv（n, from_base, to_base）`

```sql
mysql> select conv(12,10,2),conv(101101,2,16),conv('a',16,10);
+---------------+-------------------+-----------------+
| conv(12,10,2) | conv(101101,2,16) | conv('a',16,10) |
+---------------+-------------------+-----------------+
| 1100          | 2D                | 10              |
+---------------+-------------------+-----------------+
1 row in set (0.00 sec)
```

### IP转换

`inet_aton(expr)`返回一个代表该地址值的整数

```sql
mysql> select inet_aton('127.12.12.30');
+---------------------------+
| inet_aton('127.12.12.30') |
+---------------------------+
|                2131495966 |
+---------------------------+
1 row in set (0.01 sec)
```

计算方法：
$$
127\times256^3+12\times256^2+12\times256^1+30
$$


逆置：`inet_ntoa()`

```sql
mysql> select inet_ntoa(3292083091);
+-----------------------+
| inet_ntoa(3292083091) |
+-----------------------+
| 196.57.51.147         |
+-----------------------+
1 row in set (0.01 sec)
```

### 加锁和解锁

`get_lock(str,timeout)`,使用字符串str给定的命中创建一个锁，持续时间timeout

本节略过P170

### 重复执行指定操作

`benchmark(count,expr)`函数重复count次表达式expr，可用于计算处理mysql表达式的速度，值通常为0（时间很快不代表没有）

```sql
mysql> select benchmark(100000,password('smart'));
+-------------------------------------+
| benchmark(100000,password('smart')) |
+-------------------------------------+
|                                   0 |
+-------------------------------------+
1 row in set, 1 warning (0.02 sec)#执行十万次用时0.02s
```

### 改变字符集

`convert(... using ...)`

```sql
mysql> select charset('string'),charset(convert('string' using latin1));
+-------------------+-----------------------------------------+
| charset('string') | charset(convert('string' using latin1)) |
+-------------------+-----------------------------------------+
| gbk               | latin1                                  |
+-------------------+-----------------------------------------+
1 row in set (0.01 sec)
```

### 改变数据类型

cast(x, As type) 和 convert(x, type) 将一个类型的值转化为另一个类型

```sql
mysql> select cast(100 as char(2));
+----------------------+
| cast(100 as char(2)) |
+----------------------+
| 10                   |
+----------------------+
1 row in set, 1 warning (0.00 sec)
```

### case语句

```sql
mysql> select * from member;
+------+--------+-------+---------------------+-----------+
| m_id | m_fn   | m_ln  | m_birth             | m_info    |
+------+--------+-------+---------------------+-----------+
|    1 | halen  | park  | 1988-12-02 00:00:00 | Good man! |
|    2 | Samuel | Green | 2022-04-13 16:19:09 | boomer!   |
+------+--------+-------+---------------------+-----------+
2 rows in set (0.00 sec)

mysql> select last_insert_id();
+------------------+
| last_insert_id() |
+------------------+
|                2 |
+------------------+
1 row in set (0.01 sec)

mysql> select m_birth, case when year(m_birth)<2000 then 'old'
    -> when year(m_birth) >2000 then 'young'
    -> else 'not born' end as status from member;
+---------------------+--------+
| m_birth             | status |
+---------------------+--------+
| 1988-12-02 00:00:00 | old    |
| 2022-04-13 16:19:09 | young  |
+---------------------+--------+
2 rows in set (0.01 sec)
```

### 复习题

```sql
#1.从字符串“Nice to meet you!”获取字串"meet"
mysql> select substring('Nice to meet you!',9,4);
+------------------------------------+
| substring('Nice to meet you!',9,4) |
+------------------------------------+
| meet                               |
+------------------------------------+
1 row in set (0.00 sec)
#2.将弧度pi()/4 转为角度值
mysql> select degrees(pi()/4);
+-----------------+
| degrees(pi()/4) |
+-----------------+
|              45 |
+-----------------+
1 row in set (0.00 sec)
#3.保留pi()小数点后2位
mysql> select truncate(pi(),2);
+------------------+
| truncate(pi(),2) |
+------------------+
|             3.14 |
+------------------+
1 row in set (0.01 sec)
#4.计算今天是一年的第几周
mysql> select weekofyear(curdate());
+-----------------------+
| weekofyear(curdate()) |
+-----------------------+
|                    15 |
+-----------------------+
1 row in set (0.01 sec)
#5.计算今天是一年的第几天
mysql> select dayofyear(curdate());
+----------------------+
| dayofyear(curdate()) |
+----------------------+
|                  104 |
+----------------------+
1 row in set (0.00 sec)
#6.计算今天是本周的的第几个工作日
mysql> select weekday(curdate());#注意从0开始
+--------------------+
| weekday(curdate()) |
+--------------------+
|                  3 |
+--------------------+
1 row in set (0.00 sec)
#7.计算1972-3-22出生的人今年几岁
mysql> select year('1972-3-22')-year(curdate());
+-----------------------------------+
| year('1972-3-22')-year(curdate()) |
+-----------------------------------+
|                               -50 |
+-----------------------------------+
1 row in set (0.00 sec)
#8加密解密数据
mysql> show warnings;
+---------+------+------------------------------------------------------------------------------------------------+
| Level   | Code | Message                                                                                        |
+---------+------+------------------------------------------------------------------------------------------------+
| Warning | 1287 | 'ENCODE' is deprecated and will be removed in a future release. Please use AES_ENCRYPT instead |
| Warning | 1287 | 'DECODE' is deprecated and will be removed in a future release. Please use AES_DECRYPT instead |
+---------+------+------------------------------------------------------------------------------------------------+
#9.进制转换
mysql> select conv(100,10,2);
+----------------+
| conv(100,10,2) |
+----------------+
| 1100100        |
+----------------+
1 row in set (0.00 sec)
```

## 7.查询数据
