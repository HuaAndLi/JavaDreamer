[TOC]



# 简介

第1天学习笔记

# MySQL基础

 ## 安装

自己百度一下

## 登录与退出MySQL

DOS命令行登录MySQL

```shell
登录格式1：登录本机的MySQL
	mysql -u用户名 -p密码
	示例：mysql -uroot -proot
登录格式2：登录远程的MySQL
	mysql -u用户名 -p密码 -h远程主机ip
	示例：mysql -uroot -proot -h127.0.0.1
退出MySQL
	exit或quit
	
```

个人推荐使用Navicat进行管理

## DDL操作数据库和表

```mysql
/*  DDL操作数据库  */
-- 查看所有数据库
SHOW DATABASES;

-- 直接创建数据库db1,db2
CREATE DATABASE db1;

CREATE DATABASE db2;

-- 判断是否存在并创建数据库db2,db3
CREATE DATABASE IF NOT EXISTS db1;


-- 判断是否存在并创建数据库db4
CREATE DATABASE IF NOT EXISTS db3;
	
CREATE DATABASE IF NOT EXISTS db4;

-- 删除db4数据库 -- 你看行，我看刑
DROP DATABASE db4;


-- 判断数据库存在才删除db4,db3
DROP DATABASE IF EXISTS db4;

DROP DATABASE IF EXISTS db3;

-- 切换数据库到db1
USE db2;

/*  DDL操作表  */

/*
创建商品表(goods)包含: 
	商品名称(name),
	商品价格(price),
	商品销量(sales_volume),
	商品生产日期(produced_date)
*/
CREATE TABLE goods(
	NAME VARCHAR(10),
	price DOUBLE,
	sales_volume INT,
	produced_date DATE
);


/*
需求：设计一张学生表，请注重数据类型、长度的合理性
	编号，			整数
	姓名，			姓名最长不超过10个汉字
	性别，			因为取值只有两种可能，因此最多一个汉字
	生日，			取值为年月日
	入学成绩，		小数点后保留两位
	邮件地址，		最大长度不超过 64
	家庭联系电话，	不一定是手机号码，可能会出现 - 等字符，20位以内
*/
CREATE TABLE student2(
	id INT,
	NAME VARCHAR(10),
	sex CHAR(1),
	birthday DATE,
	score DOUBLE(5,2),
	email VARCHAR(64),
	phone VARCHAR(20)
);

-- 查看db1数据库中的所有表
SHOW TABLES;
-- 查看表结构
SHOW TABLES;

-- 直接删除表student表
DROP TABLE student;

-- 将goods改名成goods2
ALTER TABLE goods RENAME TO goods2;

-- 为goods2表添加一个新的字段img,类型为varchar(20)
ALTER TABLE goods2 ADD img VARCHAR(20);

-- 将goods2表中的img字段的改成varchar(100)
ALTER TABLE goods2 MODIFY img VARCHAR(100);
DESC goods2;
-- 将goods2表中的img字段名改成icon，类型varchar(80)
ALTER TABLE goods2 CHANGE img icon VARCHAR(80);
DESC goods2;
-- 删除goods2表中的字段icon
ALTER TABLE goods2 DROP icon;


```

## DML数据的增删改

```mysql
/* DML操作表中记录 */
-- 插入数据, 给指定列添加数据 给goods表添加一条数据 NAME='格力空调', price=3699
-- 注意:在MySQL中字符串可以使用""或'', 建议''
INSERT INTO goods (NAME,price) VALUES ('格力空调',3699);

-- 插入数据, 所有的字段名都写出来(少数做法)
-- 注意:日期使用''
INSERT INTO goods (NAME,price,sales_volume,produced_date) VALUES ('华为P40',5999,1000,'2020-08-20');


-- 插入数据, 插入所有字段不写字段名(常用做法)
-- '小米11', 4999, 300, '2021-03-22'
-- Column count doesn't match value count at row 1 值的数量不对应
INSERT INTO goods VALUES ('小米11',4999,300, '2021-03-22');


-- 扩展:一条SQL语句加入多条数据, VALUES 后面可以跟多个(), 一个()对应一条数据
-- 'iPhone 12', 6799, 12000, '2020-10-28'
-- 'DELL 7590', 8799, 300, '2019-06-18'
-- '立白洗衣粉', 12.9, 39000, '2018-02-13'
INSERT INTO goods VALUES 
('iPhone 12', 6799, 12000, '2020-10-28'),
('DELL 7590', 8799, 300, '2019-06-18'),
('立白洗衣粉', 12.9, 39000, '2018-02-13');


-- 不带条件修改数据，将所有的price改成0
UPDATE goods SET price = 0;


-- 带条件修改数据，把name为'华为P40'的商品price改成5999
UPDATE goods SET price = 5999 WHERE NAME = '华为P40';


-- 一次修改多个列，把name为'小米11'的商品price改成3999, sales_volume改成10000
UPDATE goods SET price = 3999,sales_volume = 10000 WHERE NAME = '小米11';


-- 带条件删除数据，删除name为'小米11'的数据
DELETE FROM goods WHERE NAME = '小米11';


-- 不带条件删除数据，删除表中的所有数据
DELETE FROM goods;
```

## 查询数据

```mysql
/*  DQL查询记录  */

-- 准备数据
CREATE TABLE goods2 (
  NAME VARCHAR(10),
  price DOUBLE,
  sales_volume INT,
  produced_date DATE,
  category VARCHAR(20)
);

INSERT INTO goods2 VALUES 
('华为P40',5999,1000,'2020-08-20','手机'),
('小米11',4999,5000,'2020-12-28','手机'),
('红米K30',2999,22000,'2020-03-11','手机'),
('糯米',8.99,200,'2016-06-08','食物'),
('米糊',7.99,30,'2013-11-22','食物'),
('iPhone 12',6799,12000,'2020-10-28','手机'),
('DELL 7590',8799,300,'2019-06-18','电脑'),
('立白洗衣粉',12.9,39000,'2018-02-13','日用品'),
(NULL,88,666,NULL,NULL),
('联想电脑',8799,700,'2017-03-13','电脑'),
('惠普电脑',8799,50,'2008-12-13','电脑');

-- 查询goods2表中的 name 和 price 列
SELECT NAME,price FROM goods2;

-- 细节:查询只是查看数据,不会修改表中数据 幂等性
-- 查询goods2表中所有字段
SELECT NAME,price,sales_volume,produced_date,category FROM goods2;


-- 查询所有字段, 使用*代表所有列, 列就是字段
SELECT * FROM goods2;

-- 我们学习是一般使用*这样查询简单快速,实际工作中,你需要什么字段就查询什么字段.


-- 添加一条相同的数据: '立白洗衣粉', 12.9, 39000, '2018-02-13','日用品'
INSERT INTO goods2 VALUES ('立白洗衣粉', 12.9, 39000, '2018-02-13','日用品');
INSERT INTO goods2 VALUES ('立白洗衣液', 12.9, 39000, '2018-02-13','日用品');

-- 去除重复查询: DISTINCT
SELECT DISTINCT NAME FROM goods2;


-- 扩展:查询每个商品的销售额price * sales_volume
SELECT price * sales_volume FROM goods2;

-- 扩展:所有商品价格打8折
SELECT price * 0.8 FROM goods2;

-- 查询goods2表中的 name 和 price 列
-- name列的别名为 商品名称，price列的别名为 价格
SELECT NAME AS 商品名称,price AS 价格 FROM goods2;

-- 取别名时AS关键字可以省略
SELECT NAME 商品名称,price 价格 FROM goods2;

-- 条件查询
-- 查询price大于1000的商品
SELECT * FROM goods2 WHERE price > 1000;

-- 查询sales_volume小于5000的商品
SELECT * FROM goods2 WHERE sales_volume < 5000;

-- 查询price不等于6799的商品
SELECT * FROM goods2 WHERE price != 6799;

-- 逻辑运算符
-- 查询price大于1000且sales_volume小于500的商品(两个条件同时满足)
SELECT * FROM goods2 WHERE price >1000 AND sales_volume < 500;
SELECT * FROM goods2 WHERE price > 1000 && sales_volume < 500;

-- 查询price大于8000 或 sales_volume小于100的商品(两个条件其中一个满足)
SELECT * FROM goods2 WHERE price > 8000 OR sales_volume < 100;

-- 查询name是华为P40和小米11和米糊的商品
SELECT * FROM goods2 WHERE NAME = '华为P40' OR NAME = '小米11' OR NAME = '米糊';

-- in: 在...里面,只要是满足()里面的数据都可以
-- 查询name是 华为P40 和 小米11 和 米糊 的商品
SELECT * FROM goods2 WHERE NAME IN ('华为P40','小米11','米糊');

-- 扩展:查询name不是华为P40和小米11和米糊的商品
SELECT * FROM goods2 WHERE NAME NOT IN ('华为P40','小米11','米糊');

-- 范围: BETWEEN 值1 AND 值2 -- 表示从值1到值2范围，包头又包尾
-- 查询price大于等于1000，且小于等于5000的商品
SELECT * FROM goods2 WHERE price BETWEEN 1000 AND 5000;
-- 细节: between 值1 and 值2, 小的写前,面大的写后面

-- 扩展:查询商品名称是null的商品
SELECT * FROM goods2 WHERE NAME IS NULL;

-- 扩展:查询商品名称不是null的商品
SELECT * FROM goods2 WHERE NAME IS NOT NULL;


-- 模糊查询like
-- 查询米开头的商品
SELECT * FROM goods2 WHERE NAME LIKE '米%';

-- 查询商品名称中包含'米'字的商品
SELECT * FROM goods2 WHERE NAME LIKE '%米%';

-- 扩展:查询名称第二个字为米的商品
SELECT * FROM goods2 WHERE NAME LIKE '_米%';


-- 扩展:查询名称最后字为米的商品
SELECT * FROM goods2 WHERE NAME LIKE '%米';

-- 扩展:查询商品名称为4个字的
SELECT * FROM goods2 WHERE NAME LIKE '____';


/*  查询排序  */
-- order by 表示排序, ASC升序, DESC降序

-- 单列排序
-- 查询所有数据,使用price升序排序
SELECT * FROM goods2 ORDER BY price ASC;

-- 查询所有数据,使用price降序排序
SELECT * FROM goods2 ORDER BY price DESC;


-- order by 默认是升序
SELECT * FROM goods2 ORDER BY price;

-- 组合排序
-- 查询所有数据,在price降序排序的基础上，如果price相同再以sales_volume降序排序
SELECT * FROM goods2 ORDER BY price DESC,sales_volume DESC;


-- 聚合函数
-- SELECT 聚合函数(字段) FROM 表名;

-- 查询商品个数, 如果字段内容为null，是不会被统计的
SELECT COUNT(NAME) FROM goods2;

-- count(*)表示所有列中，只要有一列有数据，就能被统计进来
SELECT COUNT(*) FROM goods2;
-- SELECT COUNT (*) FROM goods2; 聚合函数和(*)之间不要有空格

-- 扩展用法：统计price大于1000的总个数
SELECT COUNT(*) FROM goods2 WHERE price > 1000;

-- 查询所有商品总销量
-- 总销量是把所有商品的销量加起来
SELECT SUM(sales_volume) FROM goods2;

-- 查询销量最低的商品
SELECT MIN(sales_volume)xx FROM goods2;

-- 查询销量最高的商品
SELECT MAX(sales_volume) FROM goods2;


-- 查询商品平均价格
SELECT AVG(price) FROM goods2;


-- 扩展:让小数显示指定的位数(2位)
-- ROUND(数据, 小数位数)
SELECT ROUND(AVG(price),2) FROM goods2;


-- 注意:查询聚合函数时无法同时查出同行的其它数据，需要使用之后学习的子查询



/*  分组查询  */
-- 按商品类型分组
SELECT category FROM goods2 GROUP BY category;

-- 分组后会返回每组的第一条数据 mysql8.0版本默认会报错
-- 通常我们只获取分组字段
SELECT * FROM goods2 GROUP BY category;

-- 分组后通常是为了统计,分组后聚合函数操作每一组的数据

-- 查询每种类型的商品数量
SELECT category,COUNT(*) FROM goods2 GROUP BY category;
-- select * from goods2 order by category;
-- SELECT * FROM goods2 group BY price;

-- 查询销量大于100的商品,按商品类型分组,统计每组的数量 筛选要在分组之前
SELECT category,COUNT(*) FROM goods2 WHERE sales_volume > 100 GROUP BY category;

-- 查询销量大于100的商品,按商品类型分组,统计每组的数量,并只显商品类型数量大于2的数据
-- having 也是用来做筛选的，但是一般都是分组后，和聚合函数一起使用
SELECT 
  category,
  COUNT(*) 
FROM
  goods2 
WHERE sales_volume > 100 
GROUP BY category 
HAVING COUNT(*) > 2 ;


-- 查询商品表中数据，跳过前面2条，显示3条
SELECT * FROM goods2 LIMIT 2,3;

-- 假设我们一每页显示3条记录的方式来分页，SQL语句如下：
-- 第一页: 跳过0条, 获取3条
SELECT * FROM goods2 LIMIT 0,3;
-- 如果跳过的条数是0,可以省略
SELECT * FROM goods2 LIMIT 3;

-- 第二页: 跳过3条, 获取3条
SELECT * FROM goods2 LIMIT 3,3;

-- 第三页: 跳过6条, 获取3条
SELECT * FROM goods2 LIMIT 6,3;

-- 第四页: 跳过9条, 获取3条
SELECT * FROM goods2 LIMIT 9,3;

-- 计算公式：起始索引 = (当前页码-1)  *  每页显示的条数


```









