---
title: Mysql数据库之——表的约束
categories: MySql
copyright: true
date: 2019-04-17 16:00:43
tags:
- MySql表的约束
---
# 概念
> 对表中的数据进行限定，从而保证数据的正确性、有效性、完整性

### 约束的分类
- 主键约束：primary key
	> 
	> 注意事项：
	> 1、它自带**非空**且**唯一**
	> 2、主键就是表中的唯一标识
	> 3、一张表只能有一个字段为主键
- 非空约束：not null
- 唯一约束：unique
	> 注意：限定的值可以有多个null
- 外键约束：foreign key

<!--more-->


### 添加约束的方式
- 1、在创建表是在数据类型后面接上约束
- 2、使用修改表的命令修改


### 对表的约束操作
例子：利用修改表来删除**非空约束**
```
ALTER TABLE student MODIFY name VARCHAR(20);
ps：通用方法，特殊的下面给出了
```

例子：利用修改表来**添加约束**
```
ALTER TABLE student MODIFY name VARCHAR(20) NOT NULL;

-- 添加相关约束时，必须保证该字段的数据要全部满足相关约束的要求
ps：通用方法
```

例子：利用修改表来删除**唯一约束**
```
ALTER TABLE student DROP INDEX phone_number;
```
例子：利用修改表来删除**主键约束**
```
ALTER TABLE student DROP PRIMARY KEY;
```

### 自动增长
> 如果某一列是数值类型的，使用 `auto_increment`
> 
> 注意事项：
> 1、自动增长是看上一条记录的值

### 外键约束
概述：比如一张表中有很多冗余的数据（重复的数据），我们可以通过外键把这张表拆分为两张表，一张主表记录主要的信息，一张副表用来保存冗余的信息，在主表中可以给某个字段定义一个外键，关联到副表对应的主键中，就好比学生与老师，他们都有名字与年龄，但是职业不同，我们就可以把名字与年龄这种主要信息放在主表中，职业的相关信息就放在副表中，然后主表中每个人的信息都通过外键关联一个自己对应的职业即可。


- 语法：
	> constraint 外键名称 foreign key 外键列的字段名称 references 主表列的字段名称（外键关联到的表，通常为id）

- 删除外键

```
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

- 创建表后添加外键（创建时直接添加即可）

```
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY 外键列的字段名称 REFERENCES 主表列的字段名称（外键关联到的表，通常为id）；
```


### 外键约束的级联操作
概述：当副表中的id改变的时候，我们也希望主表中的外键也跟着变化，那么我们就需要用到级联操作了，删除同理。

- 级联更新：ON UPDATA CASCADE
- 级联删除：ON DELETE CASCADE

ps：在添加外键时，后接级联操作即可
- 注意事项：
	> 1、在使用级联操作时，要谨慎考虑，因为会影响效率，也会大面积的影响相关数据，一个操作不好容易引起数据缺失
	> 2、级联更新和级联删除可以同时添加，两个接一起即可

例子：id被删除后，外键自动设置为null
```
ALTER TABLE `class_message` ADD CONSTRAINT `FK_week_1` FOREIGN KEY (`week_id_1`) REFERENCES `creation_message` (`id`) ON DELETE SET NULL ON UPDATE CASCADE; 
```