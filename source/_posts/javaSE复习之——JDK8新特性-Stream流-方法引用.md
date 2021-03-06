---
title: javaSE复习之——JDK8新特性_Stream流_方法引用
categories: JavaSE 复习
copyright: true
date: 2019-04-11 17:12:04
tags:
- Stream流方法引用
- Stream流
- 方法引用
---
# 方法引用
> 它主要是对Lambda表达式的一种优化，在我们使用Lambda表达式的时候，我们实际上传递进去的代码是一种解决方案，比如拿什么参数做什么。
> 
> 但是有一种情况：
> 如果我们在Lambda中所使用的一种方案，在其他地方已经存在相同的方案，那么我们还需要再写重复的逻辑了嘛？？？

<!--more-->

#### 举个例子
> 我们创建一个函数式接口，这个接口专门打印字符串，那么我们使用Lambda时需要的代码量就比较多
#### 代码示例（反例）

```
//这里创建一个函数式接口
@FunctionalInterface
public interface Printable {
	void print(String str);
}


public class Demo01PrintSimple {
	//一个静态方法，传入的参数是一个接口
	private static void printString(Printable data) {
		data.print("Hello, World!");
	}

	//使用Lambda表达式，实现打印字符串
	public static void main(String[] args) {
		printString(s ‐> System.out.println(s));
	}
}
```

#### 使用Lambda中的方法引用优化上例的代码
```
public class Demo02PrintRef {
	private static void printString(Printable data) {
		data.print("Hello, World!");
	}

	public static void main(String[] args) {
		printString(System.out::println);
		//因为系统自带了就有打印字符串的实现，所以我们可以不需要使用Lambda去写功能的实现，而是直接调用已经实现好的。
	}
}

```

#### 方法引用符：“：：”
> 双冒号`：：`为引用运算符，它所在的表达式被称为**`方法引用`**。如果Lambda要表达的函数方案已经存在于某个方法的实现中，我们就可以通过双冒号来引用该方法作为Lambda的代替者

#### 上面两个案列的`语义分析`
- **`s -> System.out.println(s)`**
	> 拿到参数后经过Lambda，传递给System.out.println方法处理

- **`System.out::println`**
	> 直接让System.out中的println方法来取代Lambda


#### 使用**对象的引用名**来引用成员方法
- 首先我们有一个接口

```
@FunctionalInterface
public interface Printable {
	void print(String str);
}

```

- 然后我们有一个实现功能的类

```
public class MethodRefObject {
	public void printUpperCase(String str) {
		System.out.println(str.toUpperCase());
	}
}
```

- 当我们使用lambda，并且在Lambda中具体实现功能时，需要创建MethodRefObject类时，我们可以直接先创建类，然后直接引用它

```
public class Demo04MethodRef {
	private static void printString(Printable lambda) {
		lambda.print("Hello");
	}
	public static void main(String[] args) {
		MethodRefObject obj = new MethodRefObject();
		printString(obj::printUpperCase);
		//我们不需要在Lambda中创建类，然后调用，我们直接引用它即可
	}
}
```


#### 通过类目引用**静态成员**

> 由于在 java.lang.Math 类中已经存在了静态方法 abs ，所以当我们需要通过Lambda来调用该方法时，有两种写
法。

- 定义一个函数式接口

```
@FunctionalInterface
public interface Calcable {
	int calc(int num);
}

```

- 第一种写法是使用Lambda表达式：

```
public class Demo05Lambda {
	private static void method(int num, Calcable lambda) {
		System.out.println(lambda.calc(num));
	}
	public static void main(String[] args) {
		method(‐10, n ‐> Math.abs(n));
	}
}
```

- 不过我们有一种更好的写法，那就是用方法引用

```
public class Demo06MethodRef {
	private static void method(int num, Calcable lambda) {
		System.out.println(lambda.calc(num));
	}
	public static void main(String[] args) {
		method(‐10, Math::abs);
	}
}
```

- 在这两个例子中，下面两种写法是相等的
	- Lambda表达式： `n -> Math.abs(n)`
	- 方法引用： `Math::abs`



#### 通过super引用成员方法

- 定义一个函数式接口

```
@FunctionalInterface
public interface Greetable {
	void greet();
}

```

- 父类Human类

```
public class Human {
	public void sayHello() {
		System.out.println("Hello!");
	}
}
```

- 子类Man类

```
public class Man extends Human {
	@Override
	public void sayHello() {
		System.out.println("大家好,我是Man!");
	}
	//定义方法method,参数传递Greetable接口
	public void method(Greetable g){
		g.greet();
	}
	public void show(){
		method(super::sayHello);
	}
}
```

#### 通过this引用成员方法
- 与super引用父类成员方法同理


#### 类的构造器的引用（构造方法，也就是通过引用创建对象）
- 以构造器引用使用 `类名称::new` 的格式表示。

- 首先有个Person类

```
public class Person {
	private String name;

	public Person(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}
```

- 然后创建一个Person对象的函数式接口

```
public interface PersonBuilder {
	Person buildPerson(String name);
}
```

- 通过构造器引用来调用

```
public class Demo10ConstructorRef {
	public static void printName(String name, PersonBuilder builder) {
		System.out.println(builder.buildPerson(name).getName());
	}

	public static void main(String[] args) {
		printName("赵丽颖", Person::new);
	}
}

```

- 下面两种写法是等效的：
	- Lambda表达式： `name -> new Person(name)`
	- 方法引用： `Person::new`


#### 数组构造器的引用（创建数组）
> 数组也是 Object 的子类对象，所以同样具有构造器，只是语法稍有不同


- 首先定义一个函数式接口

```
@FunctionalInterface
public interface ArrayBuilder {
	int[] buildArray(int length);
}
```

- 使用构造器引用创建数组

```
public class Demo12ArrayInitRef {
	private static int[] initArray(int length, ArrayBuilder builder) {
		return builder.buildArray(length);
	}
	public static void main(String[] args) {
		int[] array = initArray(10, int[]::new);
	}
}
```

- 下面两种写法是等效的：
	- Lambda表达式： `length -> new int[length]`
	- 方法引用： `int[]::new`