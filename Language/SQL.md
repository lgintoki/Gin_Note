# #学习时的例子以及课堂笔记

```sql
-- 创建数据库School
create database School   --不区分大小写
go  --批处理命令

--使用数据库School
use School  --注意没有关键词database
go

--删除数据库School
use master
go
drop database School    --如果数据库正在使用，不能删除
go

--模式（schema, 在SQL Server中称为架构）
--创建架构STU
create schema STU authorization dbo 
go

--删除架构
drop schema STU 
go

-- 在SQL Server 中默认的架构是dbo

--创建表（table ）是数据库中最重要的对象
--创建学生表tblStudent
create table tblStudent
(
	stuID bigint primary key, --学号，大整型，，主键(非空)
	stuName varchar(50) not null, --姓名，变长字符类型，非空
	stuSex char(2) not null,  --性别，定长字符类型，非空
	stuBirth datetime null, --出生日期，日期时间类型，可空
	stuPhone char(11),    --电话号码, 默认可空
	stuDept varchar(20)     --系别
)
go

-- 定长：char(10)     存放：   zhangsan
--变长：varchar(10) 存放：zhangsan


--创建课程表
create table tblCourse
(
	couID char(3) primary key,  --课号
	couName varchar(20) not null unique, -- 课名，定义唯一性
	couProperty char(10) not null,  --性质
	couCredit int --学分
)
go

--创建选课表
create table tblChoose
(
	stuID bigint references tblStudent(stuID), --学号，外键
	couID char(3) references  tblCourse(couID),--课号，外键
	grade int null, --成绩
	primary key(stuID,couID)  --主键，表级约束
)
go

--修改表（对表添加、删除列，修改数据类型等等）
--添加列：
--语法:  alter table 表名 add 新列名 数据类型 约束
--例：在学生表中添加一个字段-班号
alter table tblStudent add clsID char(10) null
go
--修改列：
--语法: alter table 表名 alter column 列名
 --例：对班号修改数据类型 
 go

 alter table tblStudent alter column clsID varchar(10)
 go

--删除列
--语法: alter table 表名 drop column 列名
--例:
alter table tblStudent drop column clsID
go

--删除表
--语法: drop table 表名
--例：删除学生表
drop table tblStudent   --A 可以删除  B不能删除
go
--答：不能直接删除，因为这个表是另外一个表的主键表，即这个表被另外一个表引用。
--如果要删除，怎么做？
--答：先删外键表，再删主键表。
drop table tblChoose
go
drop table tblStudent,tblCourse
go

--插入学生表tblstudent数据
insert into tblStudent values(2019001,'赵毅','男','2000-01-01','13888888888','计科')
insert into tblStudent values(2019002,'钱尔','女','2000-12-13','13875432112','软工')
insert into tblStudent values(2019003,'孙三','女','2000-03-03','13333333333','软工')
insert into tblStudent values(2019004,'李斯','男','2001-08-09','13423234377','软工')
insert into tblStudent values(2019005,'周午','男','1999-03-08',null,'计科')
go


--对课程表tblCourse插入数据
insert into tblCourse values('A01','英语','必修',5)
insert into tblCourse values('A02','计算机','必修',4)
insert into tblCourse values('B01','经济学','选修',2)
go
select * from tblCourse
go

insert into tblChoose values(2019001,'A01',80)
insert into tblChoose values(2019001,'A02',95)
insert into tblChoose values(2019001,'B01',85)
insert into tblChoose values(2019002,'A01',75)
insert into tblChoose values(2019002,'A02',70)
insert into tblChoose values(2019002,'B01',65)
insert into tblChoose values(2019003,'A01',50)
insert into tblChoose values(2019003,'A02',NUll)
insert into tblChoose values(2019004,'A01',NUll)
go

select * from tblChoose
go


```

```sql
-- 数据查询
语法: select 列的信息       --投影（选择哪些列）
         from 表                   --连接（多表）
		 where 查找条件     --选择（选择哪些行）
		 order by 列名        --排序 -- desc降序 --asc 升序(默认)
go

select * from tblStudent   --*表示所以列
go

--查找所以女生的信息，显示她们的姓名，性别，出生日期，
--并按年龄从小到大排序
select stuName,stuSex,stuBirth 
         from tblStudent  
		 where stuSex='女' 
		 order by stuBirth desc -- desc降序 --asc 升序(默认)
go

--查询学生表，得到所有男生的姓名和年龄。
select stuName, year(getdate())  -year(stuBirth)   --计算列，函数year()获得日期中的年份
from tblStudent
where stuSex='男'
go

--别名，使用as，as 且可省
select stuName as 姓名, year(getdate())  -year(stuBirth) as 年龄  --计算列，函数year()获得日期中的年份
from tblStudent
where stuSex='男'
go

select stuName 姓名, year(getdate())  -year(stuBirth) 年龄  --计算列，函数year()获得日期中的年份
from tblStudent
where stuSex='男'
go

--查询学生来自哪些系别？
select distinct stuDept from tblStudent  --去除重复行
go


select top 3 * from tblStudent   -- top n 显示结果中的前n行
go


--查询软工的学生的姓名
select stuName,stuDept 
from tblStudent
where stuDept='软工'
go

--查询软工的女生
select stuName,stuSex,stuDept 
from tblStudent
where stuDept='软工' and stuSex='女'   -- 与 and 或 or
go

--查询2000-1-1前出生的学生
select stuName,stuBirth
from tblStudent
where stuBirth<'2000-1-1'    --日期用单引号
go

--查询来自软工或计科的同学
select stuName,stuDept
from tblStudent
where stuDept='软工' or stuDept='计科' 
go

--方法二：
select stuName,stuDept
from tblStudent
where stuDept in('软工','计科' )
go

--查询所有姓李的同学信息
select stuName
from tblStudent
where stuName  like '李%'   -- like 表示模糊查询 李X，李XX，李XXX等

select stuName
from tblStudent
where stuName  like '李_'   -- like 表示模糊查询, “李X”
go


--对空值NULL的处理
--查找没有手机的同学
select * from tblStudent
where stuPhone is null   --判断空值 is null
go

--查找有手机的同学
select * from tblStudent
where stuPhone is not null   --判断非空值 is not null
go

--130~133是联通 134~139是移动
--哪些同学的手机是移动公司的？
select * from tblStudent
where stuPhone like '13[4-9]%'
go

--聚集函数（聚簇函数）--做统计问题
--sum() 求和，max() --求最大值，min()求最小值，
--avg() 求平均值，count() 求个数

--班上有多少人？
select count(*) 人数  from tblstudent
go
--班上的女生有多少人？
select count(*) 人数  from tblstudent
where stuSex='女'
go
--班上软工的女生有多少人？
select count(*) 人数  from tblstudent
where stuSex='女' and stuDept='软工'
go
--班上男女各多少人？
--传统做法
select count(*) 女生人数 from tblStudent
where stuSex = '女'
go
select count(*) 男生人数 from tblStudent
where stuSex = '男'
go
--分组统计
语法: select 分组列名,聚集函数       --投影（选择哪些列）
         from 表                   --连接（多表）
		 group by 分组列
go
select stuSex 性别,count(*) 人数 from tblStudent  
group by stuSex
go

--班上来自各个系别的人数
select stuDept 系别,COUNT (*)人数 from tblStudent
group by stuDept
go

--找出最小的出生日期
select min(stuBirth)  最小的出生日期 from tblStudent
go


--作业：
--1、查找2000-1-1到2001-12-31之间出生的同学信息
select * from tblStudent
where stuBirth>='2000-1-1' and stuBirth<='2001-12-31'
go

--方法二：
select * from tblStudent
where stuBirth between '2000-1-1' and '2001-12-31'
go

--2、查找所有不姓'赵'、不'姓'李' 的同学。
select stuName from tblStudent
where stuName not like '赵%' and stuName not like '李%' 
go

--3、统计来自各个系别的男女同学人数
select stuSex 性别,stuDept 系别,count(*) 人数
from  tblStudent
group by stuSex,stuDept with cube
go



```

```sql

--如何计算每个同学的平均分？
select stuID 学号,avg(grade) 平均分
from tblChoose
group by stuID
go
--找出平均分>80分的同学
--分组统计
语法: select 分组列名,聚集函数       --投影（选择哪些列）
         from 表                   --连接（多表）
		 group by 分组列
		 having 分组搜索条件
go
select stuID 学号,avg(grade) 平均分
from tblChoose
group by stuID
having avg(grade)>80     --分组搜索条件
go

--查询选修了3门及以上课程的同学
select stuID 学号,COUNT(*)课程数
from tblChoose
group by stuID
having count(*)>=3
go
--必修课和选修课各占几个学分？
select couProperty 性质,sum(couCredit) 学分
from tblCourse
group by couProperty
go

--多表查询
--查找出学生的学号、姓名和每门课程成绩
select tblStudent.stuID,tblStudent.stuName,tblChoose.couID,tblChoose.grade  --有相同列名要指明是哪个表
from tblStudent,tblChoose   --多表
where tblStudent.stuID=tblChoose.stuID --连接条件
go
--表的别名
select L.stuID,L.stuName,R.couID,R.grade  --有相同列名要指明是哪个表
from tblStudent L,tblChoose R   --多表  别名as可省,别名仅在当前批处理有效
where L.stuID=R.stuID --连接条件
go
--查询每个学生的学号、姓名、课程名及成绩
select A.stuID 学号,A.stuName 姓名,C.couName 课程,B.grade 成绩
from tblStudent A,tblChoose B,tblCourse C
where A.stuID=B.stuID AND B.couID =C.couID
go
--查询选修A02号课程且成绩在90分以上的所有学生，
--显示学生姓名，A02课程名，及成绩
select A.stuName 姓名,C.couName 课程,B.grade 成绩
from tblStudent A,tblChoose B,tblCourse C
where A.stuID=B.stuID AND B.couID =C.couID and B.couID='A02' and grade>=90
go

--查找平均成绩大于等于70分的同学姓名
select stuName 姓名,avg(grade) 平均分
from tblStudent A ,tblChoose B
where A.stuID=B.stuID
group by A.stuName
having avg(grade)>=70     --分组搜索条件
go

-- 外连接
--新建学生表1，tblStudent1
create table tblStudent1
(
	stuID bigint,
	stuName varchar(20)
)
go

insert into tblStudent1 values(1,'赵毅')
insert into tblStudent1 values(2,'倩儿')
insert into tblStudent1 values(3,'孙三')
insert into tblStudent1 values(4,'李四')
insert into tblStudent1 values(5,'周吴')
go

select * from tblStudent1
go

--创建竞赛成绩表 tblContest
create table tblContest
(
	stuID bigint,
	grade int
)
go

insert into tblContest values(1,80)
insert into tblContest values(2,90)
insert into tblContest values(3,70)
insert into tblContest values(11,95)
insert into tblContest values(12,85)
go

select * from tblContest
go

--（1）查询学生竞赛信息，要求有学生学号、姓名和成绩
-- 自然连接
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L,tblContest R
where L.stuID=R.stuID
go
-- 内连接、inner join
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L inner join tblContest R
on L.stuID=R.stuID
go


--（2）查询学生竞赛信息，要求有学生学号、姓名和成绩，没有参加竞赛的同学要显示其学号和姓名。
--左连接：
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L left join tblContest R
on L.stuID=R.stuID
go

--（3）查询学生竞赛信息，要求有学生学号、姓名和成绩，没有报名但参加了竞赛的同学要显示其成绩。
--右连接：
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L right join tblContest R
on L.stuID=R.stuID
go

--（4）要求有学生学号、姓名和成绩，没有参加竞赛的同学要显示其学号和姓名，没有报名但参加了竞赛的同学要显示其成绩。
--全连接=左连接+右连接
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L full join tblContest R
on L.stuID=R.stuID
go

-- （5）交叉连接（笛卡儿积）cross join
select L.stuID,L.stuName,R.stuID,R.grade
from tblStudent1 L cross join tblContest R
go


--找来找同一系别的两个同学
--自连接（表自己连接自己，逻辑上两张表，物理上一张表）
select L.stuDept,L.stuName,R.stuName 
from tblStudent L inner join tblStudent 
on L.stuDept=R.stuDept and L.stuID<R.stuID
go

```

```sql
--嵌套查询（子查询）
--查询年龄最小的学生姓名（出生日期最大）
select stuName,stuBirth from tblStudent      --父查询
where stuBirth=(select max(stuBirth) from tblStudent)   --子查询
go

--查询英语成绩最低的同学的姓名
select stuName from tblStudent where stuID in ( 
select stuID from tblChoose where grade =(select min(grade) from tblChoose 
where couID=(select couID from tblCourse where couName='英语' )))
go

--方法2
select stuName 
from tblStudent A,tblCourse B ,tblChoose C
where A.stuID=C.stuID and B.couID=C.couID and couName='英语' and grade =(select min(grade) from tblChoose)
go




--（1）查询每个同学必修课（英语、计算机）成绩，未参加考试的同学应显示其学号姓名。查询结果如下图所示：
select A.stuID 学号,A.stuName 姓名, B.grade 英语, C.grade 计算机
from tblStudent A left join tblChoose B on A.stuID=B.stuID and B.couID='A01'  --B、C 表作为别名，又称为临时派生表
left join tblChoose  C on A.stuID=C.stuID and C.couID='A02'
go

select A.stuID 学号,A.stuName 姓名,B.grade 英语
from tblStudent A left join 
(select stuID,grade from tblChoose where couID='A01') as B --B表作为派生表
on A.stuID=B.stuID
go  --B表的作用到此为止！

--（2）查看每个同学总分和平均分，未参加考试的同学应显示其学号姓名，并按平均分高低排序。查询结果如下图所示：
select A.stuID 学号,A.stuName 姓名, sum(grade) 总分,avg(grade) 平均分
from tblStudent A left join tblChoose B
on A.stuID=B.stuID
group by A.stuID,A.stuName
order by avg(grade) desc
go

--谓词查询：

--找出至少选修了1门课的同学
 --exists/not exists的应用
 select stuID,stuName from tblStudent 
 where exists(select *  from tblChoose where tblStudent.stuID=tblChoose.stuID)
  go
 --找出一门课程都没有选的同学
select stuID,stuName from tblStudent
 where NOT exists(select *  from tblChoose  where tblStudent.stuID=tblChoose.stuID)
  go

 --找出至少选修了1门课的同学
 --in/not in的应用
 select stuID,stuName from tblStudent
 where stuID in(select distinct stuID  from tblChoose)
 go
 --找出一门课程都没有选的同学
select stuID,stuName from tblStudent
 where stuID not in(select distinct  stuID  from tblChoose)
 go



--集合查询：
--查询软工的男生
select * from tblStudent where stuDept='软工'
intersect  -- 交
select * from tblStudent where stuSex='男'
go

select * from tblStudent where stuDept='软工' and stuSex='男'
go

--查询来自软工的学生或者男生。
select * from tblStudent where stuDept='软工'
union --并
select * from tblStudent where stuSex='男'
go

select * from tblStudent where stuDept='软工' or stuSex='男'
go

--查询来自软工但不是男生的学生。
select * from tblStudent where stuDept='软工'   
except      --差：A-B
select * from tblStudent where stuSex='男'
go

select * from tblStudent where stuDept='软工' and stuSex<>'男'
go

--数据插入(Insert)
--例：插入一个学生：2019006,吴柳,男，2000-4-5, 18612345678,网安

--语法： 
insert into 表名(列名1,列名2,……) values (列值1,列值2,...)

insert into tblStudent(stuID,stuName,stuSex,stuBirth,stuPhone,stuDept) values (2019006,'吴柳','男','2000-4-5', '18612345678','网安')
go

select * from tblStudent
go

--说明1，如果按表定义列时顺序提供所有列值,此时列名可以省去不写。
insert into tblStudent values (2019006,'吴柳','男','2000-4-5', '18612345678','网安')
go
--说明2, 提供了列名也提供列值，此时列的顺序就不重要了，但是要一一对应。
insert into tblStudent(sutName,stuSex,stuBirth,stuPhone,stuDept,stuID) values ('吴柳','男','2000-4-5', '18612345678','网安',2019006)
go
--说明3，如果是空值，要标注NULL
insert into tblStudent values (2019006,'吴柳','男','2000-4-5', NULL,'网安')
go
--说明4，可部分插入,注意列的定义，对定义非空的列，必须提供值。
insert into tblStudent(stuID,sutName,stuSex,stuBirth) values (2019006,'吴柳','男','2000-4-5')
go
--说明5，insert into 可简写为insert 
--如何快速创建女生表，并插入数据
--方法一：
--第1步：创建女生表tblFemale
create table tblFemale
(
	stuID bigint primary key,
	stuName varchar(50) not null,
	stuSex char(2) Not null,
	stuPhone char(11)
)
go
--第2步：插入数据
insert into tblFemale
select stuID,stuName,stuSex,stuPhone from tblStudent
where stuSex='女'
go

select * from tblFemale
go

-- 方法2（不用create table）
select stuID,stuName,stuSex,stuPhone
into tblFemale2      --直接利用查询的结果，创建一个新表并填充值
from tblStudent
where stuSex='女'
go

select * from tblFemale2
go

--数据删除（delete）
--语法：
delete from 表名
where 删除条件
go

--删除女生表中的孙三
delete from tblFemale
where stuName='孙三'
go

--(1) from 可省
delete tblFemale
where stuName='孙三'
go
--(2) 如果省去where,表示删除表中的所有数据
delete from tblFemale
--(3)注意与drop table 的区别
--delete 是删除表中的数据
--drop table 删除表对象

drop table tblFemale
go

select * from tblFemale
go
--(4) 注意删除时有时要考虑外键约束，如果要删除，先删除外键表中的数据，再删主键表的数据
select * from tblStudent
go
select * from tblChoose
go

delete from tblStudent 
where stuID=2019006  --成功
go  

delete from tblChoose   --先删外键表
where stuID=2019004
delete from tblStudent  --再删主键表
where stuID=2019004    
go

--（5）delete 中也可以应用子查询
select * 
into tblStudent3
from tblStudent
go
select * from tblStudent3
go

--删除tblStudent3中年龄最大的学生
delete from tblStudent3
where stuBirth=(select min(stuBirth) from tblStudent3)  --子查询
go

--数据更新（update）
--语法：
update 表名
set 列名1=新列值1,列名2=新列值2,...
where 条件   
go


--给每位考试了同学的英语成绩+5分。
update tblChoose
set grade = grade +5
where couID=(select couID from tblCourse where couName='英语') and grade is not null
go   --子查询

--把计算机课程的学分修改为6学分
select * from tblCourse
go

update tblCourse
set couCredit =6
where couName ='计算机'
go




select * from tblCourse
go

--注意：insert delete update 这些语句成功执行后，通常会显示消息：（X行受影响）

select * from tblStudent3
go


```

```sql
--创建视图
--创建视图vwGrade，根据此视图可以获得学生的姓名、课名和成绩
create view vwGrade
as 
select a.stuName ,c.couName ,b.grade 
from tblChoose b ,tblStudent a ,tblCourse c
where b.stuID  =a.stuID  and b.couID=c.couID
go

select * from vwGrade
go

select * from vwGrade   --视图(表)
where stuName='赵毅' and couName='英语'
go


--创建视图vwFemale，获得女生信息。
--并且在此视图进行插入和更新时检查是否是女生。
create view vwFemale
as
select * from tblStudent
where stuSex='女'
with check option   -- 检查选项
go

--测试，插入一个学生
insert into vwFemale 
values(2019010,'金链','女','2000-10-10',null,'网安')
go  --注意这个数据最终是放在学生表中！

select * from tblStudent
go

select * from tblStudent  --主键表
select * from tblChoose   --外键表
go

delete from tblStudent
where stuName='赵毅'    
go

delete from tblStudent
where stuName='金链'
go

--在主键表中delete/update记录，可能受到外键表约束，默认是不能删除（no action）,
--除非在定义外键时，采用了级联cascade操作。级联的含义就是delete/update主键表中的一条记录，
--对应外键表中记录也一并删除/更新。

create table tblStudent2
(
	stuID bigint primary key,
	stuName varchar(20) not null
)
go
create table tblCourse2
(
	couID char(3) primary key,
	couName varchar(20) not null
)
go
create table tblchoose2
(
	stuID bigint,
	couID char(3),
	primary key(stuID,couID),
	foreign key(stuID) references tblStudent2(stuID) on delete cascade on update cascade, --级联
	foreign key(couID) references tblCourse2(couID) on delete no action on update no action,  --拒绝(默认)
)
go

insert into tblStudent2 values (1,'赵毅')
insert into tblStudent2 values (2,'钱儿')
go
insert into tblCourse2 values('A','英语')
insert into tblCourse2 values('B','数学')
go
insert into tblChoose2 values(1,'A')
insert into tblChoose2 values(1,'B')
insert into tblChoose2 values(2,'A')
insert into tblChoose2 values(2,'B')
go

select * from tblStudent2  --主键表
select * from tblCourse2  --主键表
select * from tblChoose2   --外键表
go

--操作
update tblStudent2
set stuID=10
where stuID=1          --cascade 级联
go

delete from tblStudent2 
where stuID=10        --cascade 级联
go

update tblCourse2
set couID='D'
where couID='A'    -- no action 拒绝
go

delete from tblCourse2
where couID='A'   -- no action 拒绝
go

--创建教师表
create table tblTeacher
(
	teaID bigint primary key, --主键约束
	teaName varchar(20) not null unique, --非空约束 唯一性约束
	teaSex char(2) not null check(teaSex='男' or teaSex='女'),  --检查约束  check(teaSex in('男','女')
	teaBirth datetime check(teaBirth between '1920-1-1'and '2010-1-1'),
	teaPhone char(11),
	teaTitle varchar(10) default('讲师')
)
go

insert into tblTeacher values(101,'孙南','男','1982-12-31',13777777777,'教授')
go

insert into tblTeacher(teaID,teaName,teaSex) values(102,'李菲','女')
go

select * from tblTeacher
go

--创建授课表
create table tblTeach
(
	teaID bigint,
	couID char(3)
)
go

--可以通过修改表的方式来添加相应约束。
--基本语法：
alter table 表名
add constraint 约束名   --创建表时的约束名大多由系统自动生成了相应的约束名。
primary key()
foreign key()
unique()
check()
default
go

--给授课表添加主键
alter table tblTeach 
alter column teaID bigint not null
go

alter table tblTeach 
alter column couID char(3) not null
go

alter table tblTeach 
add constraint PK_Teach 
primary key(teaID,couID)
go

--给授课表添加外键
alter table tblTeach 
add constraint FK_teaID
foreign key(teaID) references tblTeacher(teaID)
go

alter table tblTeach 
add constraint FK_couID
foreign key(couID) references tblCourse(couID)
go

--在选课表上添加约束
alter table tblChoose
add constraint CK_grade
check(grade>=0 and grade<=100)
go

--在学生表中默认学生的系别为软工
alter table tblStudent
add constraint DF_city
default '软工' for stuDept
go



```

```sql
--局部变量的定义/声明和赋值
declare @stuName varchar(20) --局部变量的定义/声明
select @stuName='赵毅' --赋值方法1
set @stuName='赵毅'    --赋值方法2
declare @stuName varchar(20)='赵毅'  --局部变量的定义/声明和赋值
print @stuName
go

--全局变量（系统变量）
print @@servername --本地SQL Server服务器名
go

--以下是waitfor的用法看起来很好 
waitfor delay '00:00:30'--过30秒后执行以下程序  
select * from tblStudent  
waitfor time '22:48:30'--到晚上22:48:30的时候执行以下的语句   
select * from tblstudent 


--系统函数
declare @stuName char(50)   --定长50个字符
declare @stuName2 varchar(50)
select @stuName ='          zhaoyi'
set @stuName2=RTRIM(LTRIM(@stuName)) --去除最左边最右边的空格
print @stuName2
go


declare @stuID bigint
declare @stuName varchar(50)
select @stuID=2000000011101
select @stuName='zhaoyi'
print cast(@stuID as varchar)+@stuName  -- 这里+号表示两个字符串的连接
go

declare @number int
set @number=100
print sqrt(@number)
go


select getdate()

select datepart(dayofyear,getdate())

select year(getdate()) 年,month(getdate()) 月,day(getdate()) 日

select datepart(year,getdate()),datepart(month,getdate()),datepart(day,getdate()),datepart(hour,getdate()),datepart(minute,getdate()),datepart(second,getdate()),datepart(microsecond,getdate())

select datepart(yy,getdate()),datepart(mm,getdate()),datepart(dd,getdate()),datepart(hh,getdate()),datepart(MINUTE,getdate()),datepart(SS,getdate())

select datename(year,getdate()),datename(month,getdate()),datename(day,getdate()),datename(hour,getdate()),datename(minute,getdate()),datename(second,getdate()),datename(microsecond,getdate())

declare @a int
set @a=100
select  @a+'abc'




--创建用户自定义函数
--（1）标量函数
alter function fnLevelbyAvg(@avgGrade int)  --平均值参数
returns varchar(10)
as
begin
 declare @level varchar(10)  --评价变量
 if(@avgGrade>100 or @avgGrade<0)
 set @level='成绩有误'
 else if @avgGrade>=80
 set @level='优'
 else if @avgGrade>=70
 set @level='中'
 else if @avgGrade>=60
 set @level='及格'
 else
  set @level='不及格'
 return @level
end
go

-- 使用函数

select stuID 学号,avgGrade 平均分, dbo.fnLevelbyAvg(avgGrade) 评价   --函数不能向存储过程一样单独执行
from vwAvgGrade
go

--(2) 表值函数
create function fnStubyID(@stuID bigint)
returns table
as
return(
select * from tblStudent where stuID=@stuID
)
go

--使用函数
select * from dbo.fnStubyID(2009001)   --可以把函数fnStubyID看成一个带参数的表
go


--创建函数fnStuByCitySex，@city，@sex
create function fnStuByCitySex
(@city varchar(20),@sex char(2))
returns table
as
return(
select * from tblStudent
where stuDept=@city and stuSex=@sex)
go

--使用函数
select * from dbo.fnStubyCitySex('计科','女')

select count(*) from Student 
where stuID=2009001 and stuPsw='123456'
go


--存储过程
--系统存储过程

exec sp_databases  --列出所有数据库
exec sp_helpdb School  --报告指定数据库的详细信息

--用户自定义存储过程语法
create procedure 存储过程名
@参数 数据类型
as
SQL语句
go

--创建存储过程proStudentByCitySex，@city，@sex
create procedure proStudentByCitySex
@city varchar(20),
@sex char(2)
as
select * from tblStudent
where stuDept=@city and stuSex=@sex
go
--执行存储过程
exec proStudentByCitySex @city='软工',@sex='男'

exec proStudentByCitySex '软工','男'
go

--触发器
--创建触发器，在学生表中插入数据时，会提示插入学生的姓名。
create trigger triInsertStudent on tblStudent
after insert   --for insert
as
begin
	declare @stuName varchar(20)  --定义一个局部变量@stuName
	select @stuName = stuName from inserted  --逻辑表inserted，结构如同tblStudent
	print @stuName+'已经被插入学生表'
end
go

--测试
insert into tblStudent values(2019020,'高兴','男',null,null,null)
go

select * from tblStudent
go


--如果在选课表中删除多行数据时，系统提示不允许删除
create trigger triDeleteChoose on tblChoose
after delete
as
if(select count(*) from deleted)>1
begin
	raiserror('你不能一次在选课表中删除多行数据!',16,1)
	rollback tran
end
go

--测试
delete from tblChoose
where stuID=2019001
go

select * from tblChoose
go



--更新某门课成绩时，提示成绩前后的变化
create trigger trigUpdateGrade on tblChoose
for update
as
begin
	declare @stuID bigint,@couID char(3),@grade1 int,@grade2 int
	select @stuID=stuID,@couID=couID,@grade1=grade from deleted
	select @grade2=grade from inserted
	print convert(varchar(10),@stuID)+'同学，课程'+@couID+'的成绩已经从'+ltrim(@grade1)+'变成'+ltrim(@grade2)
end
go

update tblChoose
set grade=80
where stuID=2019001 and couID='A01'
go




declare @stuID int,@stuName varchar(4),@stuAge int
--创建游标
declare curTmp cursor 
for select * from tblTmp;

--打开游标
open curTmp


--利用游标读取数据
fetch next from curTmp into @stuID,@stuName,@stuAge
while @@FETCH_STATUS =0    --与fetch配合使用 0：成功；-1 失败；-2 行不存在
	begin
	    print '学号'+ltrim(@stuID)+'   姓名'+ltrim(@stuName)+'  年龄'+ltrim(@stuage)
		if @stuID%2=0
			delete from tblTmp where stuID=@stuID

		fetch next from curTmp into @stuID,@stuName,@stuAge
	end
--关闭游标
close curTmp;

--删除游标
deallocate curTmp;
go


```

# #查询

### SELECT: 用于从数据库中选择数据

```sql
· SELECT * FROM table_name;
```

### DISTINCT: 用于过滤掉重复的值并返回指定列的行

```sql
· SELECT DISTINCT column_name;
```

### WHERE: 用于过滤记录/行

```sql
· SELECT column1, column2 FROM table_name WHERE condition;
· SELECT * FROM table_name WHERE condition1 AND condition2;
· SELECT * FROM table_name WHERE condition1 OR condition2;
· SELECT * FROM table_name WHERE NOT condition;
· SELECT * FROM table_name WHERE condition1 AND (condition2 OR condition3);
· SELECT * FROM table_name WHERE EXISTS (SELECT column_name FROM table_name WHERE condition);
```

### ORDER BY: 用于结果集的排序，升序（ASC）或者降序（DESC）

```sql
· SELECT * FROM table_name ORDER BY column;
· SELECT * FROM table_name ORDER BY column DESC;
· SELECT * FROM table_name ORDER BY column1 ASC, column2 DESC;
```

### SELECT TOP: 用于指定从表顶部返回的记录数

```sql
· SELECT TOP number columns_names FROM table_name WHERE condition;
· SELECT TOP percent columns_names FROM table_name WHERE condition;
· 并非所有数据库系统都支持SELECT TOP。 MySQL 中是LIMIT子句
· SELECT column_names FROM table_name LIMIT offset, count;
```

### LIKE: 用于搜索列中的特定模式，WHERE 子句中使用的运算符

```sql
· % (percent sign) 是一个表示零个，一个或多个字符的通配符
· _ (underscore) 是一个表示单个字符通配符
· SELECT column_names FROM table_name WHERE column_name LIKE pattern;
· LIKE ‘a%’ （查找任何以“a”开头的值）
· LIKE ‘%a’ （查找任何以“a”结尾的值）
· LIKE ‘%or%’ （查找任何包含“or”的值）
· LIKE ‘_r%’ （查找任何第二位是“r”的值）
· LIKE ‘a_%_%’ （查找任何以“a”开头且长度至少为3的值）
· LIKE ‘[a-c]%’（查找任何以“a”或“b”或“c”开头的值）
```

### IN: 用于在 WHERE 子句中指定多个值的运算符

```sql
· 本质上，IN运算符是多个OR条件的简写
· SELECT column_names FROM table_name WHERE column_name IN (value1, value2, …);
· SELECT column_names FROM table_name WHERE column_name IN (SELECT STATEMENT);
```

### BETWEEN: 用于过滤给定范围的值的运算符

```sql
· SELECT column_names FROM table_name WHERE column_name BETWEEN value1 AND value2;
· SELECT * FROM Products WHERE (column_name BETWEEN value1 AND value2) AND NOT column_name2 IN (value3, value4);
· SELECT * FROM Products WHERE column_name BETWEEN #01/07/1999# AND #03/12/1999#;
```

### NULL: 代表一个字段没有值

```sql
· SELECT * FROM table_name WHERE column_name IS NULL;
· SELECT * FROM table_name WHERE column_name IS NOT NULL;
```

### AS: 用于给表或者列分配别名

```sql
· SELECT column_name AS alias_name FROM table_name;
· SELECT column_name FROM table_name AS alias_name;
· SELECT column_name AS alias_name1, column_name2 AS alias_name2;
· SELECT column_name1, column_name2 + ‘, ‘ + column_name3 AS alias_name;
```

```sql
UNION: 用于组合两个或者多个 SELECT 语句的结果集的运算符
· 每个 SELECT 语句必须拥有相同的列数
· 列必须拥有相似的数据类型
· 每个 SELECT 语句中的列也必须具有相同的顺序
· SELECT columns_names FROM table1 UNION SELECT column_name FROM table2;
· UNION 仅允许选择不同的值, UNION ALL 允许重复
```

### ANY|ALL: 用于检查 WHERE 或 HAVING 子句中使用的子查询条件的运算符

```sql
· ANY 如果任何子查询值满足条件，则返回 true。
· ALL 如果所有子查询值都满足条件，则返回 true。
· SELECT columns_names FROM table1 WHERE column_name operator (ANY|ALL) (SELECT column_name FROM table_name WHERE condition);
```

## GROUP BY: 通常与聚合函数（COUNT，MAX，MIN，SUM，AVG）一起使用，用于将结果集分组为一列或多列

```sql
· SELECT column_name1, COUNT(column_name2) FROM table_name WHERE condition GROUP BY column_name1 ORDER BY COUNT(column_name2) DESC;
```

### HAVING: HAVING 子句指定 SELECT 语句应仅返回聚合值满足指定条件的行。它被添加到 SQL 语言中，因为WHERE关键字不能与聚合函数一起使用。

```sql
· SELECT COUNT(column_name1), column_name2 FROM table GROUP BY column_name2 HAVING COUNT(column_name1) > 5;
```

# #增删改

### INSERT INTO: 用于在表中插入新记录/行

```sql
· INSERT INTO table_name (column1, column2) VALUES (value1, value2);
· INSERT INTO table_name VALUES (value1, value2 …);
```

### UPDATE: 用于修改表中的现有记录/行

```sql
· UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
· UPDATE table_name SET column_name = value;
```

### DELETE:用于删除表中的现有记录/行

```sql
· DELETE FROM table_name WHERE condition;
· DELETE * FROM table_name;
```

### ADD: 添加字段

```sql
· ALTER TABLE table_name ADD column_name column_definition;
```

### MODIFY: 修改字段数据类型

```sql
· ALTER TABLE table_name MODIFY column_name column_type;
```

### DROP: 删除字段

```sql
· ALTER TABLE table_name DROP COLUMN column_name;
```

# #聚合查询

### COUNT: 返回出现次数

```sql
· SELECT COUNT (DISTINCT column_name);
```

### MIN() and MAX(): 返回所选列的最小/最大值

```sql
· SELECT MIN (column_names) FROM table_name WHERE condition;
· SELECT MAX (column_names) FROM table_name WHERE condition;

```

### AVG(): 返回数字列的平均值

```sql
· SELECT AVG (column_name) FROM table_name WHERE condition;
```

### SUM(): 返回数值列的总和

```sql
· SELECT SUM (column_name) FROM table_name WHERE condition;
```

# #连接查询

### INNER JOIN: 内连接，返回在两张表中具有匹配值的记录

```sql
· SELECT column_names FROM table1 INNER JOIN table2 ON table1.column_name=table2.column_name;
· SELECT table1.column_name1, table2.column_name2, table3.column_name3 FROM ((table1 INNER JOIN table2 ON relationship) INNER JOIN table3 ON relationship);

```

### LEFT (OUTER) JOIN: 左外连接，返回左表（table1）中的所有记录，以及右表中的匹配记录（table2）

```sql
· SELECT column_names FROM table1 LEFT JOIN table2 ON table1.column_name=table2.column_name;
```

### RIGHT (OUTER) JOIN: 右外连接，返回右表（table2）中的所有记录，以及左表（table1）中匹配的记录

```sql
· SELECT column_names FROM table1 RIGHT JOIN table2 ON table1.column_name=table2.column_name;
```

### FULL (OUTER) JOIN: 全外连接，全连接是左右外连接的并集. 连接表包含被连接的表的所有记录, 如果缺少匹配的记录, 以 NULL 填充

```sql
· SELECT column_names FROM table1 FULL OUTER JOIN table2 ON table1.column_name=table2.column_name;
```

### Self JOIN: 自连接，表自身连接

```sql
· SELECT column_names FROM table1 T1, table1 T2 WHERE condition;
```

# #视图查询

### CREATE: 创建视图

```sql
· CREATE VIEW view_name AS SELECT column1, column2 FROM table_name WHERE condition;
```

### SELECT: 检索视图

```sql
· SELECT * FROM view_name;
```

### DROP: 删除视图

```sql
· DROP VIEW view_name;
```

