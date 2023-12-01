[TOC]



# 简介

第2天学习笔记



# MySQL高级

## 约束

- 主键约束
- 唯一约束
- 非空约束
- 默认值约束
- 外键约束

```mysql
/*
约束使用方式：
	一、可以在建完表之后再添加（很少这么干，了解）
	二、一般都是在创建表的时候直接加约束（经常）

为什么呢？
	因为当表创建完毕之后，有可能会添加数据。如果已添加的数据跟约束冲突了，那么此时约束就加不上去了。所以，我们一般是在创建表的时候就直接加约束了，因为在创建表的时候里面肯定是没有任何数据的。
*/


/* =========== 主键约束 =========== */
-- 创建表学生表st1, 包含字段(id, name, age)将id做为主键
-- 创建表时添加主键
CREATE TABLE st1 (
	id INT,
	NAME VARCHAR(10),
	age INT
);

INSERT INTO st1 VALUES (1, '刘德华', 60);
INSERT INTO st1 VALUES (2, '郭富城', 58);

-- 演示主键约束: 唯一非空


-- 删除主键约束(了解)

-- 在已有表中添加主键约束(了解)


/* =========== 主键自动增长 =========== */
-- 创建学生表st2, 包含字段(id, name, age)将id做为主键并自动增长
CREATE TABLE st2 (
	id INT,
	NAME VARCHAR(10),
	age INT
);

-- 主键默认从1开始自动增长: i++
INSERT INTO st2 (NAME, age) VALUES ('貂蝉', 28);
INSERT INTO st2 (NAME, age) VALUES ('西施', 18);
INSERT INTO st2 (NAME, age) VALUES ('王昭君', 26);
INSERT INTO st2 (NAME, age) VALUES ('杨玉环', 22);

-- 修改自动增长的开始值(面试题)



/* =========== 唯一约束 =========== */
/* =========== 非空约束 =========== */
/* =========== 默认值约束 =========== */
CREATE TABLE emp (
	id INT, -- 员工id，主键且自增长
	ename VARCHAR(50), -- 员工姓名，非空并且唯一
	joindate DATE, -- 入职日期，非空
	salary DOUBLE(7,2), -- 工资，非空
	bonus DOUBLE(7,2) -- 奖金，如果没有奖金默认为1000
);


INSERT INTO emp(id, ename, joindate, salary, bonus) values(1, '张三', '1999-11-11', 8800, 5000);
INSERT INTO emp(id, ename, joindate, salary, bonus) values(2, '李四', '1999-11-11', 8800, 5000);

-- 演示非空约束
INSERT INTO emp(id, ename, joindate, salary, bonus) values(3, null, '1999-11-11', 8800, 5000);

-- 演示唯一约束
INSERT INTO emp(id, ename, joindate, salary, bonus) values(3, '李四','1999-11-11', 8800, 5000);

-- 演示默认约束
INSERT INTO emp(id, ename, joindate, salary) values(3, '王五', '1999-11-11', 8800);



-- 面试题: 主键是唯一和非空，普通的字段我们也可以添加唯一和非空,有区别吗?
/*
一张表只有一个主键
一张表可以有多个唯一非空的字段
*/




/* =========== 外键约束约束 =========== */
-- 准备数据: 见PPT
-- 创建部门表
CREATE TABLE department (
	id INT PRIMARY KEY AUTO_INCREMENT,
	dep_name VARCHAR(20),
	dep_location VARCHAR(20)
);

-- 创建员工表
CREATE TABLE employee (
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(20),
	age INT,
	dep_id INT
);

-- 添加2个部门
INSERT INTO department (dep_name, dep_location) VALUES ('研发部', '广州'), ('销售部', '深圳');

-- 添加员工,dep_id表示员工所在的部门
INSERT INTO employee (NAME, age, dep_id) VALUES 
('张三', 20, 1),
('李四', 21, 1),
('王五', 20, 1),
('老王', 20, 2),
('大王', 22, 2),
('小王', 18, 2);


-- 删除从表 employee
DROP TABLE employee;

-- 创建 employee 并添加外键约束



-- 正常添加数据


-- 添加不正常的数据,报错: Cannot add or update a child row: a foreign key constraint fails  

-- 删除外键约束(了解)

-- 在已有表添加外键约束, 外键约束可以省略: CONSTRAINT 外键约束名 (了解)
-- 省略CONSTRAINT外键约束名 数据库会自动设置外键约束的名字,我们要到 `3信息` 中查找


```

## 事务

## 多表查询

```mysql
/*  多表查询  */

-- 准备数据
-- 创建部门表
CREATE TABLE tb_dept (
  id INT PRIMARY KEY AUTO_INCREMENT,
  NAME VARCHAR(20)
);

INSERT INTO tb_dept (NAME) VALUES ('开发部'),('市场部'),('财务部'),('销售部');


-- 创建员工表
CREATE TABLE tb_emp (
  id INT PRIMARY KEY AUTO_INCREMENT,
  NAME VARCHAR(10),
  gender CHAR(1),   -- 性别
  salary DOUBLE,   -- 工资
  join_date DATE,  -- 入职日期
  dept_id INT
);

INSERT INTO tb_emp(NAME,gender,salary,join_date,dept_id) VALUES('孙悟空','男',7200,'2013-02-24',1);
INSERT INTO tb_emp(NAME,gender,salary,join_date,dept_id) VALUES('猪八戒','男',3600,'2010-12-02',2);
INSERT INTO tb_emp(NAME,gender,salary,join_date,dept_id) VALUES('唐僧','男',9000,'2008-08-08',2);
INSERT INTO tb_emp(NAME,gender,salary,join_date,dept_id) VALUES('白骨精','女',5000,'2015-10-07',3);
INSERT INTO tb_emp(NAME,gender,salary,join_date,dept_id) VALUES('蜘蛛精','女',4500,'2011-03-14',1);
INSERT INTO tb_emp VALUES (NULL, '白龙马', '男', 1, '2020-02-02', NULL);

-- 查询孙悟空员工的信息, 包括所在的部门名称
SELECT dept_id FROM tb_emp WHERE NAME = '孙悟空';
SELECT NAME FROM tb_dept WHERE id = (SELECT dept_id FROM tb_emp WHERE NAME = '孙悟空'); 
SELECT * FROM tb_emp,tb_dept;

-- 去掉笛卡尔积
-- 去掉笛卡尔积的条件称为: 表连接条件
SELECT * FROM tb_emp,tb_dept WHERE tb_emp.dept_id = tb_dept.id;

-- 在加上查询员工名字为孙悟空
SELECT * FROM tb_emp,tb_dept WHERE tb_emp.`dept_id` = tb_dept.id AND tb_emp.`NAME` = '孙悟空';

-- 扩展:给表取别名,表取了别名后,只能使用别名啦!
SELECT * FROM tb_emp e,tb_dept d WHERE e.`dept_id` = d.`id` AND e.`NAME` = '孙悟空';

/* ===========显式内连接=========== */
-- 显式内连接 INNER JOIN...ON
-- 查询孙悟空员工的信息, 包括所在的部门名称
-- INNER可以省略,初学者不建议省略
SELECT 
  * 
FROM
  tb_emp 
  INNER JOIN tb_dept 
    ON tb_emp.`dept_id` = tb_dept.`id` 
WHERE tb_emp.`NAME` = '孙悟空' 

/* ===========左外连接查询=========== */
-- 左外连接查询 (满足要求的显示,保证左表不满足要求的也显示)
/* ===========右外连接=========== */
-- 右外连接
-- 查询所有员工信息，即使没有分配部门的员工，也要查询出来
SELECT * FROM tb_emp LEFT OUTER JOIN tb_dept ON tb_emp.`dept_id` = tb_dept.id

-- 查询所有的部门信息，包括部门的人员信息，如果部门没有人员，也查询出来
SELECT * FROM tb_emp RIGHT OUTER JOIN tb_dept ON tb_emp.`dept_id` = tb_dept.id;

  -- 一般在工作中我们都使用左外, 右外可以转成左外, 我们中国人的书写顺序,从左到右
-- SELECT * FROM tb_dept RIGHT OUTER  JOIN tb_emp ON tb_emp.`dept_id` = tb_dept.id;
  
  
  /* ===========子查询结果=========== */
  -- 子查询结果的三种情况
-- 1.单行单列(一个值)
-- 2.多行单列(多个值)
-- 3.多行多列 (虚拟的表)

  /* ===========子查询的结果是单行单列=========== */
  -- 查询工资最高的员工是谁？
  -- 查询工资最高的是多少
  SELECT MAX(salary) FROM tb_emp;   -- 9000
  -- 根据工资，查询对应的员工是谁
  SELECT * FROM tb_emp WHERE salary = (SELECT MAX(salary) FROM tb_emp);
 
  /* ===========子查询的结果是多行单列的时候=========== */
  -- 查询工资大于5000的员工, 来自于哪些部门的名字
  -- 查询工资大于5000的员工的部门id
  SELECT dept_id FROM tb_emp WHERE salary > 5000; -- 1,2
  -- 查询对应的部门名字
  SELECT NAME FROM tb_dept WHERE id IN (SELECT dept_id FROM tb_emp WHERE salary > 5000);
  
  /* ===========子查询的结果是多行多列=========== */
  -- 查询出2011年以后入职的员工信息, 包括部门名称
  -- 想要查询所有员工的信息，以及对应的部门信息
  SELECT * FROM tb_emp LEFT OUTER JOIN tb_dept ON tb_emp.`dept_id` = tb_dept.id;
  
  -- 查询出2011年以后入职的员工信息
  SELECT * FROM tb_emp WHERE join_date >= '2011-01-01';
  -- 关联查询出对应的部门信息
SELECT 
  * 
FROM
  (SELECT 
    * 
  FROM
    tb_emp 
  WHERE join_date >= '2011-01-01') e 
  LEFT OUTER JOIN tb_dept 
    ON e.`dept_id` = tb_dept.id ;

  
  
  
  
/* ===========多表查询练习=========== */
-- 准备数据
-- 部门表
CREATE TABLE dept (
  id INT PRIMARY KEY,
  -- 部门id
  dname VARCHAR (50),
  -- 部门名称
  loc VARCHAR (50) -- 部门位置
) ;

-- 添加4个部门
INSERT INTO dept(id,dname,loc) VALUES 
(10,'教研部','北京'),
(20,'学工部','上海'),
(30,'销售部','广州'),
(40,'财务部','深圳');

-- 职务表, 职务名称, 职务描述
CREATE TABLE job (
  id INT PRIMARY KEY,
  jname VARCHAR(20),
  description VARCHAR(50)
);

-- 添加4个职务
INSERT INTO job (id, jname, description) VALUES
(1, '董事长', '管理整个公司, 接单'),
(2, '经理', '管理部门员工'),
(3, '销售员', '向客人推销产品'),
(4, '文员', '使用办公软件');

-- 员工表
CREATE TABLE emp (
  id INT PRIMARY KEY, -- 员工id
  ename VARCHAR(50), -- 员工姓名
  job_id INT, -- 职务id
  mgr INT , -- 上级领导
  joindate DATE, -- 入职日期
  salary DECIMAL(7,2), -- 工资
  bonus DECIMAL(7,2), -- 奖金
  dept_id INT, -- 所在部门编号
  CONSTRAINT emp_jobid_ref_job_id_fk FOREIGN KEY (job_id) REFERENCES job (id),
  CONSTRAINT emp_deptid_ref_dept_id_fk FOREIGN KEY (dept_id) REFERENCES dept (id)
);

-- 添加员工
INSERT INTO emp(id,ename,job_id,mgr,joindate,salary,bonus,dept_id) VALUES 
(1001,'孙悟空',4,1004,'2000-12-17','8000.00',NULL,20),
(1002,'卢俊义',3,1006,'2001-02-20','16000.00','3000.00',30),
(1003,'林冲',3,1006,'2001-02-22','12500.00','5000.00',30),
(1004,'唐僧',2,1009,'2001-04-02','29750.00',NULL,20),
(1005,'李逵',4,1006,'2001-09-28','12500.00','14000.00',30),
(1006,'宋江',2,1009,'2001-05-01','28500.00',NULL,30),
(1007,'刘备',2,1009,'2001-09-01','24500.00',NULL,10),
(1008,'猪八戒',4,1004,'2007-04-19','30000.00',NULL,20),
(1009,'罗贯中',1,NULL,'2001-11-17','50000.00',NULL,10),
(1010,'吴用',3,1006,'2001-09-08','15000.00','0.00',30),
(1011,'沙僧',4,1004,'2007-05-23','11000.00',NULL,20),
(1012,'李逵',4,1006,'2001-12-03','9500.00',NULL,30),
(1013,'小白龙',4,1004,'2001-12-03','30000.00',NULL,20),
(1014,'关羽',4,1007,'2002-01-23','13000.00',NULL,10);

-- 工资等级表
CREATE TABLE salarygrade (
  grade INT PRIMARY KEY,
  losalary INT,
  hisalary INT
);

-- 添加5个工资等级
INSERT INTO salarygrade(grade,losalary,hisalary) VALUES 
(1,7000,12000),
(2,12010,14000),
(3,14010,20000),
(4,20010,30000),
(5,30010,99990);


-- 多表查询规律
-- 1.根据需求明确查询哪些表
-- 2.明确表连接条件去掉笛卡尔积
-- 3.后续的查询


-- 练习1
-- 查询有职务的员工信息。显示员工编号, 员工姓名, 工资, 职务名称, 职务描述
-- 1.根据需求明确查询哪些表 emp job
SELECT * FROM emp,job;
-- 2.明确表连接条件去掉笛卡尔积
SELECT * FROM emp INNER JOIN job ON emp.`job_id` = job.`id`
-- 3.后续的查询
SELECT 
emp.id AS 员工编号,
emp.`ename` AS 员工姓名,
emp.`salary` AS 工资,
job.`jname` AS 职务名称,
job.`description` AS 职务描述
FROM emp INNER JOIN job ON emp.`job_id` = job.`id`


-- 练习2
-- 查询有职务和部门的员工信息。显示员工编号, 员工姓名, 工资, 职务名称, 职务描述, 部门名称, 部门位置
-- 1.根据需求明确查询哪些表 emp job dept
SELECT * FROM emp,job,dept;
-- 2.明确表连接条件去掉笛卡尔积
SELECT * FROM emp 
INNER JOIN job ON emp.`job_id` = job.id 
INNER JOIN dept ON emp.`dept_id` = dept.`id`;
-- 3.后续的查询
SELECT 
emp.`id` 员工编号,
emp.`ename` 员工姓名,
emp.`salary` 工资,
job.`jname` 职务名称,
job.`description` 职务描述,
dept.`dname` 部门名称,
dept.`loc` 部门位置
FROM emp 
INNER JOIN job ON emp.`job_id` = job.id 
INNER JOIN dept ON emp.`dept_id` = dept.`id`;



-- 练习3
-- 查询有部门的经理的信息。显示员工姓名, 工资, 职务名称, 职务描述, 部门名称, 部门位置, 工资等级
-- 1.根据需求明确查询哪些表 emp,job,dept,salarygrade
-- 2.明确表连接条件去掉笛卡尔积
-- 3.后续的查询
SELECT
emp.`ename` 员工姓名,
emp.`salary` 工资,
job.`jname` 职务名称,
job.`description` 职务描述,
dept.`dname` 部门名称,
dept.`loc` 部门位置,
salarygrade.`grade` 工资等级
FROM emp 
INNER JOIN job ON emp.`job_id` = job.`id`
INNER JOIN dept ON emp.`dept_id` = dept.`id`
INNER JOIN salarygrade ON emp.`salary` BETWEEN salarygrade.`losalary` 
AND salarygrade.`hisalary`
WHERE job.`jname` = '经理';







-- 练习4
-- 查询出所有部门编号、部门名称、部门位置、部门人数
-- 1.根据需求明确查询哪些表 dept,emp
SELECT * FROM dept INNER JOIN emp;
-- 2.找到表连接条件，去掉笛卡尔积
SELECT * FROM dept INNER JOIN emp ON dept.id = emp.dept_id;
-- 3.后续的查询
SELECT 
dept.`id` 部门编号,
dept.`dname` 部门名称,
dept.`loc` 部门位置,
COUNT(emp.`dept_id`) 部门人数
 FROM dept 
LEFT OUTER JOIN emp ON dept.id = emp.dept_id 
GROUP BY dept.`id`;


-- 练习5
-- 列出所有员工的姓名及其直接上级领导的姓名, 没有上级领导的员工也需要显示,显示自己的名字和领导的名字
-- 1.根据需求明确查询哪些表 emp,emp
-- Not unique table/alias: 'emp'
-- select * from emp inner join emp;
SELECT * FROM emp pt INNER JOIN emp ld
-- 2.明确表连接条件去掉笛卡尔积
SELECT * FROM emp pt LEFT OUTER JOIN emp ld ON pt.`mgr` = ld.id;
-- 3.后续的查询
SELECT 
pt.`ename` 自己的名字,
ld.`ename` 领导的名字
FROM emp pt 
LEFT OUTER JOIN emp ld ON pt.`mgr` = ld.id;





```

