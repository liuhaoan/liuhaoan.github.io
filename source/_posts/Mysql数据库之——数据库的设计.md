---
title: Mysql数据库之——数据库的设计
categories: MySql
copyright: true
date: 2019-04-18 09:08:47
tags:
- 数据库的设计
- 数据库的备份和还原
- 数据库的三大范式
---
# 多表之间的关系
- 一对一（了解）
	> 比如：学生与学号
	> 分析：一个学生只能有一个学号，一个学号只能对应一个学生

- 一对多（多对一）
	> 比如：学生和班级
	> 分析：一个学生只能在一个班级中，一个班级可以有多个学生

- 多对多
	> 比如：学生和课程
	> 分析：一个学生可以有多个课程，一个课程也可以被多个学生学习

<!--more-->

# 实现它们之间的关系
- 一对多（多对一）
	> 在多的一方建立外键，只想一的一方的主键
	> 例如：一个学生的信息表中，可以定义一个外键指向班级信息表中的主键

- 多对多
	> 多对多的关系需要建立一张中间表来实现
	> 实现方法：
	> 在中间表中必须有两个以上字段，这两个字段都是外键，并且分别对应着另外两张表的主键

- 一对一
	> 任意一方添加外键指向另一张表的主键，并且外键必须加唯一约束。
	> 然而问题来了。。。。
	> 既然是一对一，它们是唯一的，那么为什么不合成一张表，而多此一举做两张表呢。。所以一对一关系用的很少


# 数据库的设计范式（三大范式）
> 设计数据库时，需要遵循的一些规范

设计关系数据库时，遵循不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，越高的范式数据库冗余越小

#### 目前关系数据库有6种范式
- 第一范式（1NF）
- 第二范式（2NF）
- 第三范式（3NF）
- 巴斯-科德范式（BCNF）
- 第四范式（4NF）
- 第五范式（5NF又称为完美范式）

ps：通常我们用到的是前三大范式，做到了这三大范式，我们的数据库设计就几乎没什么问题了

# 三大范式的要求
- 第一范式
	> 每个列都是原子列，也就是不能一个列分成两个列，或者说多个字段不能合并成一个字段

- 第二范式：在1NF的基础上，非码属性必须完全依赖于码，也就是消除非主属性对主码的部分依赖
	>  1、**函数依赖**：A --> B,如果通过A属性（属性组）的值，可以确定一个唯一B属性的值，则成B依赖于A
	>  例如：学号 --> 姓名          （学号，课程名称） --> 分数
	>  
	>  2、**完全函数依赖**：A --> B,如果A是一个属性组，则B属性值得确定需要依赖于A属性组中所有的属性值，则B依赖于A
	>  例如：（学号，课程名称） --> 分数
	>  
	>  3、**部分函数依赖**：A --> B,如果A是一个属性组，则B属性值的确定只需要依赖于A属性组中某一些值即可
	>  例如：（学号，课程名称） --> 姓名
	>  
	>  4、**传递函数依赖**：A --> B , B --> C.如果通过A属性（属性组）的值，可以确定B属性的值，再通过B属性(属性组)的值可以确定唯一C属性的值，则称C传递函数依赖于A
	>  
	>  5、**码**：如果在一张表中，一个属性或者属性组，被其他所有属性所完全依赖，则称这个属性（属性组），为该表的码
	>  主属性：码属性组中的所有属性
	>  非主属性：除去码属性组的属性

- 第三范式：在2NF的基础上，任何非主属性不依赖与其他非主属性（也就是在2NF基础上消除传递依赖）

总结：第一范式让所有字段都是原子项，第二范式就是消除部分依赖，第三范式就是消除传递依赖


# 数据库的备份和还原
- 备份
	> mysqldump -u用户名 -p密码 数据库名称 > 保存的路径

- 还原：
	> 1、登入数据库
	> 2、创建数据库
	> 3、使用数据库
	> 4、执行文件 source 文件路径