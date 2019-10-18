---
layout: post
title: "java和python"
date: 2019-10-11
tags: java
---

# java和python

## 区分变量是静态类型还是动态类型,是强类型还是弱类型
```
静态类型：编译的时候就知道每一个变量的类型。
动态类型：编译的时候不知道每一个变量的类型，运行时进行类型检查和绑定。
强类型：不容忍隐式类型转换。
弱类型：容忍隐式类型转换。

强类型、静态类型 ：Java
强类型、动态类型 ：Python
```

## 基本类型和封装类型

java:
```
byte(1字节)		Byte
short(2字节)		Short
int(4字节)		Integer
long(8字节)		Long
float(4字节)		Float
double(8字节)	Double
char(2字节)		Character
boolean(未定)	Boolean
```

python
```
number(int、float、bool、complex)
String
list
tuple
set
dict
```

## 传递引用还是传递值

java:
```
对于基本类型变量，Java是传值的副本；
对于引用类型变量，即所有的对象型变量，Java都是传引用的副本。
```

python:
```
如果函数收到的是一个可变对象（比如字典或者列表）的引用，就能修改对象的原始值－－相当于通过“传引用”来传递对象。
如果函数收到的是一个不可变对象（比如数字、字符或者元组）的引用，就不能直接修改原始对象－－相当于通过“传值'来传递对象。
```

## 字符串的实现方式和种类

### 创建字符串
java:`String name = "xiao";`

python:`name = "xiao`

### 访问字符串中的值
java:`name.charAt(2)`

python:`name[2]`

### 连接字符串
java:`s1.concat(s2);`或`s1+s2`

python:`s1+s2`

### 格式化字符串
java:
```
System.out.printf("My name is %s, age is %d", "xiao", 25);
String str = String.format("My name is %s", "xiao");
```

python:
```
print("My name is %s, age is %d" % ("xiao", 25))
print("My name is {}, age is {}".format("xiao", 25))
```

### 内建函数
```
						python				java
第一个字符大写		capitalize()
空格填充且居中		center(width)
指定字符的数量		count(str,beg,end)
编码					encode(encoding="")
解码					decode(encoding="")
检查结尾				endswith()				endsWith()
检查开头				startswith()			startsWith
tab符转空格			expandtabs()
查找返回索引			find()
查找返回索引(右侧)		rfind()
查找返回索引			index()					indexOf()
查找返回索引(右侧)		rindex()				lastIndexOf
格式化字符串			format()

是否由字母数字组成		isalnum()
是否由字母文字组成		isalpha()
是否只包含十进制数字	isdecimal()
是否只包含数字		isdigit()
是否都是大写字母		isupper()
是否都是小写字母		islower()
是否只包含数字字符		isnumeric()
是否只包含空格		isspace()
是否是标题化的		istitle()

字符合并				join()					concat()
左对齐填充至n长度		ljust(width)
右对齐填充至n长度		rjust(width)
大写转小写			lower()					toLowerCase
小写转大写			upper()					toUpperCase
去除左右字符(空格)		strip()					trim()
去除左侧字符(空格)		lstrip()
去除右侧字符(空格)		rstrip()
创建字符映射的转换表	maketrans(s1, s2)
返回最大字母			max()
返回最小字母			min()
分割字符串			partition(str)
分割字符串(右侧)		rpartition(str)
切割字符串			split()					split()
替换					replace()				replace()
大小写翻转			swapcase()
标题化				title()
0为开头填充至n		zfill(width)

						java
返回位置的值			charAt(index)
对比					compareTo()
对比，忽略大小写		cpmpareToIgnoreCase()
比较					equals()
比较，忽略大小写		equalsIgnoreCase()
相同顺序字符时true	contentEquals
编码为 byte 序列		getBytes()
返回哈希码			hashCode()
规范化表示形式		intern()
是否匹配给定的正则		matches()
替换匹配正则的str		replaceAll()
替换匹配正则的第一str	replaceFirst()
返回新的字符序列		subSequence()
截取区间字符			substring()
返回字符数组			toCharArray()
```

## 容器

### 容器对象的种类与实现原理

java:
Collection接口:
```
	--List有序，可重复
		- ArrayList
		优点: 底层数据结构是数组，查询快，增删慢。
		缺点: 线程不安全，效率高

		- Vector
		优点: 底层数据结构是数组，查询快，增删慢。
		缺点: 线程安全，效率低

		- LinkedList
		优点: 底层数据结构是链表，查询慢，增删快。
		缺点: 线程不安全，效率高

	--Set无序，唯一，都不是线程安全的，如果要使用线程安全可以Collections.synchronizedSet()，HashSet插入数据最快，其次LinkHashSet，最慢的是TreeSet因为内部实现排序
		- HashSet，底层数据结构是哈希表。(无序,唯一)
		保证元素唯一性依赖两个方法：hashCode()和equals()
		主要功能：通用的存储数据的集合，允许存在null

		- LinkedHashSet，底层数据结构是链表和哈希表。(FIFO插入有序,唯一)
		1.由链表保证元素有序
		2.由哈希表保证元素唯一
		主要功能：用于保证FIFO即有序的集合(先进先出)，允许存在null

		- TreeSet，底层数据结构是红黑树。(唯一，有序)
		1.保证元素排序：自然排序、比较器排序
		2.保证元素唯一性：根据比较的返回值是否是0来决定
		主要功能：用于排序，插入null数据会报NullPointerException

	--Queue
```

```
Map:
	--HashMap		无序，不同步，线程不安全，效率高，允许null值，父类是AbstractMap
	--TreeMap		有序
	--HashTable		无序，同步，线程安全，效率低，不允许null值，父类是Dictionary
```

### 容器的遍历

- List:
```
//for
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
System.out.println("----------");

//foreach
for (Integer i : list) {
    System.out.println(i);
}
System.out.println("----------");

//iterator
Iterator it = list.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
System.out.println("----------");


for i in list:
    print(i, end=" ")
print()

for i in range(len(list)):
    print(list[i], end=" ")

for i, j in enumerate(list):
    print(i, j)
```

- set
```
//foreach
for (Integer integer : set) {
    System.out.println(integer);
}
System.out.println("--------------");

//iterator
Iterator it = set.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

```
for i in set:
    print(i, end=" ")
print()

for i, j in enumerate(set):
    print(i, j)
```

- map/dict
```
//keySet
Set<Integer> set = map.keySet();
for (Integer i : set) {
    System.out.println(i + ":" + map.get(i));
}
System.out.println("---------------");

//entrySet
Set<Map.Entry<Integer, String>> ss = map.entrySet();
Iterator it = ss.iterator();
while (it.hasNext()) {
    Map.Entry e = (Map.Entry) it.next();
    System.out.println(e.getKey() + ":" + e.getValue());
}
```

```

for i in dict:
    print(i, dict[i])
print("--------")

for i in dict.items():
    print(i)
print("--------")

for i, j in dict.items():
    print(i, j)
print("--------")

for key in dict.keys():
    print(key, dict[key])
print("--------")

for value in dict.values():
    print(value)
print("--------")

```

- tuple
```
for i in tuple:
    print(i, end=" ")

for i, j in enumerate(tuple):
    print(i, j)

for i in iter(tuple):
    print(i, end=" ")

```

### 容器深浅复制

python:
对于数字和字符串，赋值、浅拷贝、深拷贝在内存当中用的都是同一块地址
对于字典、列表、元组等其他类型，赋值的内存地址不会变化。
对于字典、列表、元组等类型，浅拷贝只拷贝第一层地址。
对于字典、列表、元组等类型，深拷贝它里面嵌套多少层，就会拷贝多少层出来，但是最底层的数字和字符串地址不变。

使用浅拷贝修改新的字典的值之后，原来的字典里面的cpu值也被修改了
深拷贝的时候，只有新的字典的cpu值被修改了，原来的字典里面的cpu值没有变

java:
浅拷贝：对基本数据类型进行值传递，对引用数据类型进行引用传递般的拷贝，此为浅拷贝。
深拷贝：对基本数据类型进行值传递，对引用数据类型，创建一个新的对象，并复制其内容，此为深拷贝。

### 容器的序列化与反序列化

python:
```
with open("./file/list.txt", "wb") as f:
    pickle.dump(list, f)

with open("./file/list.txt", "rb") as f:
    print(pickle.load(f))
```

java:
```
ObjectOutputStream oos =
                new ObjectOutputStream(
                        new FileOutputStream("a.txt"));
oos.writeObject(list);

ObjectInputStream ois =
				new ObjectInputStream(
						new FileInputStream("a.txt"));
System.out.println(ois.readObject().toString());
```

### 常用容器操作函数


List
```
|---------------------------------------------------|
|			|	java		|		python			|
|-----------+---------------+-----------------------|
|末尾添加元素	|add()			|	append(e)			|
|索引添加元素	|add(index, e)	|	insert(index,e)		|
|删除索引元素	|remove(index)	|	pop()/pop(index)	|
|删除某个元素	|remove(e)		|	remove(e)			|
|获取索引元素	|get(index)		|	list[index]			|
|包含元素个数	|size()			|	len(list)			|
|清空列表		|				|	clear()				|
|拷贝		|				|	copy()				|
|指定数据数量	|				|	count(e)			|
|查找元素位置	|				|	index()				|
|列表合并		|				|	extend()			|
|反转		|				|	reverse()			|
|排序		|				|	sort()				|
|---------------------------------------------------|
```

Set
```
|---------------------------------------------------|
|			|	java		|		python			|
|-----------+---------------+-----------------------|
|添加元素		|add()			|		add(e)			|
|删除元素		|remove(e)		|  remove(e)/discard(e)	|
|是否包含元素	|contains(e)	|						|
|最大值		|				|		max()			|
|随机删除		|				|		pop()			|
|清空		|clear()		|		clear()			|
|拷贝		|				|		copy()			|
|判断包含		|contains()		|						|
|判断为空		|isEmpty()		|						|
|---------------------------------------------------|
```

Map/Dict:
```
|---------------------------------------------------|
|			|	java		|		python			|
|-----------+---------------+-----------------------|
|添加元素		|put(k,v)		|		dict[k]=v		|
|获取元素		|get(k,v)		|						|
|删除		|remove(k)		|	pop(k)/popitem()	|
|清空		|clear()		|		clear()			|
|修改		|				|		update(k=v)		|
|查找		|				|		get(k)			|
|判断包含该键	|containsKey(k)	|						|
|判断包含该值	|containsValue(v)|						|
|提取key		|keySet()		|		keys()			|
|提取value	|values()		|		values()		|
|提取k,v		|entrySet()		|		items()			|
|---------------------------------------------------|
```

## 编程语言实现抽象的方法、类、对象、接口与函数的实现、使用

### 函数的定义与调用
### 函数的参数使用与传递方式(是否有特殊规则如默认参数,多参同名函数,函数运算符重载等)
### 类和对象的实现方式,语言是否内置面向对象的设计模式支持
### 是多继承还是接口,接口是否需要显示声明(提前声明)
### 常⻅的设计模式实现,如单例模式,代理模式(委托),观察者模式

## 函数式编程
### 高阶函数对象

python:
```
res = sorted(list,reverse=False,key=func)
res = map(func,list)
res = reduce(func,tuple)
res = filter(func,tuple)
```

### 语法特性与编程习惯(如链式语法,闭包等)
java8新特性:
```
Lambda表达式
 
函数式接口
 
Stream
 
Optional
 
Predicate
 
Function
 
Consumer
 
Filter
 
Map-Reduce
 
新的Date API
```