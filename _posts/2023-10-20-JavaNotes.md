---
layout: post
title: 'Java Notes'
date: 2023-10-24
author: Liyang
cover: 'https://images.unsplash.com/photo-1653629154302-8687b83825e2'
cover_author: 'rogov'
cover_author_link: 'https://unsplash.com/@rogovca'
tags: 
- Java 
- Notes 
pin: true
---

## commonJavaAPI 

### 1.Objects类中常用方法

```java
/*
1.用于判断两个对象是否相等。
Object.equals方法容易抛空指针异常，应该使用常量或者确定的值来调用equals。
如果是两个变量比较时，就都需要加非空判断，
因为Object.equals方法内调用的是 return( this == obj ) 。
而Objects.equals方法中就做了非空判断，故不会抛出空指针异常。
*/
public static boolean equals(Object a, Object b){
	return (a == b) || (a != null && a.equals(b));
}
//2.判空方法，如果参数为空则返回true。
public static boolean inNull(Object obj){
	return obj == null;
}
//3.非空判断，如果参数不为空则返回true。
public static boolean nonNull(Object obj){
    return obj != null;
}
```

### 2.包装类

&emsp;&emsp;将基本数据类型的数据包装为对象。

```java
//	基本				包装
		byte				Byte
		short				Short
		int					Integer
/*
	valueof(int i);
	该方法将一个int类型的数字封装成Integer的一个对象，是创建Integer对象的常用方法。
	Integer integer = Integer.valueOf(6)
*/
		long				Long
		float				Float
		double			Double
		boolean			Boolean
		char				Character
```

### 3.其他方法
```java
//1.将基本数据类型转化为字符串
public String toString();
//例如：String s = Integer.toString(i);
//2.将字符串类型的数值转换为数值本身对应的数据类型
public static Integer valueof(String s);
//例如：double d = Double.valueof(str);
```

## StringBuilder & StringBuffer

&emsp;&emsp;StringBuilder 支持链式编程，在频繁的拼接、修改字符串时，其效率远远高于String。

&emsp;&emsp;StringBuffer的用法和StringBuilder的用法一毛一样。因此下面只展示StringBuilder的用法。

&emsp;&emsp;但是StringBuilder是线程不安全的，而StringBuffer是线程安全的。

```java
//1.构造器
//1.1.创建一个空白可变字符串对象， 不含有任何内容
public StringBuilder();
//1.2.根据字符串的内容，来创建可变字符串对象
public StringBuilder(String str): 
//2.常用方法
//2.1.添加数据
public StringBuilder append(任意类型);
//2.2.将对象内容反转
public StringBuilder reverse();
//2.3.返回对象内容长度
public int length();
//2.4.将StringBuilder转换为String
public String toString();
```

## StringJoiner

&emsp;&emsp;JDK8开始才有，类似于StringBuilder，用于操作字符串。

```java
//1.构造器
//1.1.创建一个StringJoiner对象，指定拼接时的间隔符号。
public StringJoiner(间隔符号);
//1.2.创建一个StringJoiner对象，指定拼接时的符号。
public StringJoiner(间隔付哈，开始符号，结束符号);
//2.常用方法
//2.1.添加数据，并返回对象本身。
public StringJoiner add(添加内容);
//2.2.返回长度(字符出现的个数)
public int length();
//2.3.返回一个字符串(该字符串就是拼接后的结果)
public String toString();
```

## Math & System & Runtime

### Math

&emsp;&emsp;数学，是一个工具类。

```java
//常用方法
//1.获取参数绝对值
public static int abs(int i);
//2.向上取整
public static double ceil(double a);
//3.向下取整
public static double floor(double a);
//4.四舍五入
public static int round(float a);
//5.获取最大值
public static int max(int a, int b);
//6.返回a的b次幂
public static double pow(double a, double b);
//7.返回值为[0.0 , 1.0)的double随机值
public static dooble random();
```

### System

&emsp;&emsp;代表程序所在的系统，是一个工具类。

```java
//1.终止JVM
public static void exit(int status);
/*
status 为 0：表示正常退出程序，也就是结束当前正在运行中的java虚拟机。
status 为 1 或 -1 或 任何其他非零值 ：表示非正常退出当前程序。
正常退出:是指如果当前程序还有在执行的任务，则等待所有任务执行完成以后再退出；
非正常退出:是只要时间到了，立刻停止程序运行，不管是否还有任务在执行。
*/
//2.以毫秒返回系统时间。
//此方法返回当前时间与1970年1月1日午夜 UTC（协调世界时）之间的差异，以毫秒为单位。
public static long currentTimeMillis();
```

### Runtime

&emsp;&emsp;代表程序所在的运行环境，是一个单例类。

```java
//1.返回与当前Java应用程序关联的运行时对象。
public static Runtime getRuntime();
//2.终止当前运行的虚拟机,该参数用作状态代码。按照惯例，非零的状态码表示异常终止。
public void exit(int status);
//3.获取虚拟机可以使用的处理器数量。
public int availableProcessors();
//4.返回JVM中的内存总量
public long totalMemory();
//5.返回JVM中的可用内存量
public long freeMemory();
//6.启动某个程序，并返回代表该程序的对象。
public Process exec(String command);
```

## BigDecimal

&emsp;&emsp;通常用于解决大数运算和浮点数运算失真问题。

```java
//1.构造器
//1.1.把字符串转换成BigDecimal
public BigDecimal(String val);
//2.常用方法：
//2.1.将double转化为BigDecimal
public static BigDecimal valueOf(double val);
//2.2.加
public BigDecimal add(BigDecimal b);
//2.3.减
public BigDecimal subtract(BigDecimal b);
//2.4.乘
public BigDecimal multiply(BigDecimal b);
//2.5.除
public BigDecimal divide(BigDecimal b);
public BigDecimal divide(BigDecimal b,精确到几位，舍入模式);
//2.6.将BigDecimal转换为double
public double doubleValue();
```

## 日期 & 时间

### JDK8之前

#### Date

```java
//1.构造器
//1.1.创建Date对象，代表系统当前的此刻日期时间。
public Date();
//2.把时间毫秒值转换为Date对象。
public Date(long time); 
//2.常用方法
//2.1.返回1970年1月1日到此刻的总毫秒数
public long getTime();
//2.2.设置日期对象的时间为当前时间
public void setTime();
```

#### SimpleDateFormat

&emsp;&emsp;简单日期格式化。

```java
//1.常用构造器
//1.1.创建简单日期格式化对象，并封装时间格式
public SimpleDateFormat(String pattern);
//2.常用方法
//2.1.将日期格式化成 日期/时间 字符串
public final String format(Date date);
//2.2.将时间毫秒值格式化成 日期/时间 字符串
public final String format(Object time);
//2.3.把字符串时间解析成日期对象
public Date parse(String source);
```

#### Calendar

&emsp;&emsp;抽象类，代表系统此刻时间对应的日历。通过它可以单独获取、修改时间中的年、月、日、时、分、秒等。

```java
//常用方法
//1.获取当前日历对象
public static Calendar getInstance();
//2.获取日历中的某个信息
public int get(int field);
//3.获取日期对象
public final Date getTime();
//4.获取时间毫秒值
public long getTimeInMillis();
//5.修改日历的某个信息
public void set(int field, int value);
//6.为某个信息 增加/减少 指定的值
public void add(int field, int amount);
```

### JDK8之后

#### LocalDate & LocalTime & LocalDateTime

&emsp;&emsp;LocalDate:代表本地日期(Y,M,D,W);&emsp;W:星期

&emsp;&emsp;LocalTime:代表本地时间(H,M,S,NS);&emsp;NS:纳秒

&emsp;&emsp;LocalDateTime:代表本地日期时间(Y,M,D,W,H,M,S,NS);

```java
//1.获取对象的方法
//获取系统当前时间对应的对象
public static LocalDate now();
public static LocalTime now();
public static LocalDateTime now();
/*
示例：
LocalDate ld = LocalDate.now();
LocalTime lt = LocalTime.now();
LocalDateTime ldt = LocalDateTime.now();
*/
//2.常用方法：太多了。。。。不想写。。。。以后有时间会补
/*
常用方法包含：加(plus)、修改(with)、减(minus)、相等(equals)、在前(isBefore)、在后(isAfter)等几大类。
三者方法类似，使用方式相同。
注意：JDK8新增的日期时间创建的对象是无法被修改的，调用以上方法时会返回新的日期时间对象。
*/
```

#### ZoneId &ZoneDateTime

&emsp;&emsp;JDK8后新增加的，ZoneId：时区；ZoneDateTime：带时区的时间。



