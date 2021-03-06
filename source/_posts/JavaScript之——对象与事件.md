---
title: JavaScript之——对象与事件
categories: JavaScript
copyright: true
date: 2019-05-07 16:23:32
tags:
- 对象
- DOM
- BOM
- JavaScript事件
---

# 对象
### 基本对象
##### Function
> 函数（方法）对象，在js中函数（方法）就是一个对象

- 创建：
	- 第一种方法：`var fun = new Function(形式参数列表， 方法体);`（忘了吧）
	- 第二种方法：`function 方法名称(形式参数列表) {方法体};`
	- 第三种方法：`var fun = function(形式参数列表) {方法体};`
- 属性：
	- length：代表形参的个数
- 特点（重要）
	- 定义方法时，形参的类型不用写，返回值类型也不用写，因为都是var，写不写都无所谓。
	- 方法时一个对象，如果定义了名字相同的方法，那么就会被覆盖
	- 在JS中，方法的调用只与方法的名字有关，和它的参数无关
	- 在方法声明中有一个隐藏的内置对象（数组），argument，封装了所有传入的实际参数，也就是说调用方法传多少参数都行
- 调用

<!--more-->

#### Array
> 数组对象

- 创建
	- 第一种方法：var arr = new Array(元素列表);
	- 第二种方法：var arr = new Array(默认长度);
	- 第三种方法：var arr = [元素列表];

- 方法：
	- join():将数组中的元素按照指定的分隔符拼接为字符串
	- push():在数组尾部添加元素，返回新的长度
- 属性：
	- length：数组长度
- 特点：
	- JS中，数组元素的类型是可变的
	- JS中，数组的长度是可变的，访问多少索引，数组长度就是访问的索引自动加1

#### Date
- 创建：**`var data = new Data();`**
- 方法
	- toLocaleString()：返回当前对象对应的时间本地字符串格式
	- getTime()：获取毫秒值，返回当前日期对象描述的时间到1970年1月1日0点的毫秒值差

#### Math
- 创建：**`不用换创建，直接使用 Math.方法名();`**
- 属性：
	- PI：圆周率
- 方法：
	- random()：返回0 - 1之间的随机数，含0不含1
	- ceil()：对数进行下舍入（向上取整数）
	- floor()：对数进行下舍入（向下取整数）
	- round()：把数四舍五入为最近的整数


#### RegExp
> 正则表达式对象

- 正则表达式：定义字符串的组成规则

- 单个字符：[]
	- [a]：a
	- [ab]：a或b
	- [a-zA-Z0-9]:a到z 或 A-Z 或 0-9
	- \d:单个数字字符：[0-9]
	- \w:单个单词字符：[a-zA-Z0-1]

- 量词符号：
	- ？：表示出现0次或1次
	- *：表示出现0次或多粗
	- +：出现一次或者多次
	- {m,n}：表示长度m到n，m <= 数量 <= n
		- m如果缺省：{,n}:最多n次
		- n如果缺省：{m,}：最少m次

- 开始结束符号
	- ^ : 开始
	- $ : 结尾


- 正则对象
	- 创建
		- **`var reg = new RegExp("正则表达式");`**
		- **`var reg = /正则表达式/;`**
	- 方法
		- test():验证指定的字符串是否符合正则定义的规范


#### Global
> 它是一个全局对象，Global对象中封装的方法不需要对象就可以直接调用。

- 方法
	- encodeURI()：url编码
	- decodeURI()：url解码
	- 
	- encodeURIComponent()：url编码（编码更多一些，它可以对/等进行编码）
	- decodeURIComponent()：url解码
	- 
	- parseInt():将字符串转为数字，它逐一判断每一个字符是否是数字，直到不是数字为止，然后将前面数字部门转成number
	- isNaN():判断一个值是否是NaN
		- 为什么需要这个方法呢？ 答：NaN六亲不认，甚至连自己都不认，所以需要一个方法来判断是否是NaN
	- **`eval():将 JavaScript 字符串转为脚本来运行，重要一定要知道`**

- 什么是url编码？
	- 我们在通过浏览器进行数据传输的，而传输数据是用协议传输的，而协议是不支持中文数据的，而我们需要将中文的数据传输到服务器中，就需要进行一个转码的动作，我们经常是用url编码完成，而浏览器默认用的也是url编码方式

#### Boolean
#### Number
#### String