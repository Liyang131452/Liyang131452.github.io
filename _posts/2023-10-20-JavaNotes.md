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



## 前言：

&emsp;&emsp;这是一篇关于自学Java的杂记。如有问题或者不对，请给我发邮件，我进行更正。邮箱：bryceyangli@gmail.com

## commons

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

#### ZoneId & ZoneDateTime

&emsp;&emsp;JDK8后新增加的，ZoneId：时区；ZoneDateTime：带时区的时间。

```java
//1.获取Java支持的全部时区ID
public static Set<String> getAvailableZoneIds();
//2.把某个时区ID封装成ZoneId对象
public static ZoneId of(String ZoneId);
//3.获取系统默认时区
public static ZoneId systemDefault();
```

#### Instant

&emsp;&emsp;时间线上的某个 时刻 / 时间戳 。用于替代Date。

```java
//1.获取当前时间的Instant对象(标准时间)
public static Instant now();
//2.获取从1970年1月1日0分0秒开始记录的秒数
public long getEpochSecond();
//3.从时间线开始，获取从第二个开始的纳秒数
public int getNano();
//4.作为参数传递的秒/纳秒/毫秒值添加到此瞬时，并将结果作为瞬时对象返回。且此返回的Instant是不可变的。
public Instant plusSeconds(long secondsToAdd);
public Instant plusNanos(long nanosToAdd);
public Instant plusMillis(long millisToAdd);
//5.将此Instant与作为参数传递的Instant对象进行比较,如果两个实例相等，则返回true。
public boolean equals(Object otherInstant);
//6.检查此瞬间是否在指定瞬间之前。如果此时刻在指定时刻之前，则返回true。
public boolean isBefore(Instant otherInstant);
//7.检查此瞬间是否在指定瞬间之后。如果此时刻在指定时刻之后，则返回true。
public boolean isAfter(Instant otherInstant);
```

#### DateTimeFormatt

&emsp;&emsp;格式化器，用于时间格式化解析。**新增原因：SimpleDateFormat线程不安全。**

```java
//1.获取格式化器对象
public static DateTimeFormatter ofPattern(时间格式);
//2.格式化时间
public String format(时间对象);
```

#### Period & Duration

&emsp;&emsp;Period：计算日期间隔；用于计算两个LocalDate对象相差的年、月、日数。

```java
//1.传入两个日期对象，得到Period对象
public static Period between(LocalDate start, LocalDate end);
//2.计算并返回相隔几年
public int getYears();
//3.计算并返回相隔几月
public int getMonths();
//4.计算并返回相隔几日
public int getDays();
```

&emsp;&emsp;Duration：计算时间间隔; 用于计算两个时间对象相差天、小时、分、秒、纳秒数；支持LocalTime、LocalDateTime、Instant等时间。

```java
//1.传入两个时间对象，得到Duration对象
public static Duration between(开始时间对象，截止时间对象);
//2.计算并返回相隔 天 数
public long toDays();
//3.计算并返回相隔 小时 数
public long toHours();
//4.计算并返回相隔 分钟 数
public long toMinutes();
//5.计算并返回相隔 秒 数
public long toSeconds();
//6.计算并返回相隔 毫秒 数
public long toMillis();
//7.计算并返回相隔 纳秒 数
public long toNanos();
```

## Arrays类

&emsp;&emsp;用于操作数组的一个工具类。

```java
//常见方法
//1.返回数组的内容
public static String toString(类型[] arr);
//2.拷贝数组(指定范围，包前不包后)
public static <T> T[] copyOfRange(T[] original, int from, int to);
//3.拷贝数组,若被拷贝的数组数据不够，其余由null补充
public static <T> T[] copyOf(T[] original, int newLength);
//4.使用提供的生成函数来计算每个元素，设置指定数组的所有元素。
public static <T> void setAll(T[] array, IntFunction<? extends T> generator);
public static void setAll(double[] array, IntToDoubleFunction generator);
//5.对数据进行排序(默认升序排序)
public static void sort(T[] arr);
```

### 实现两个对象的比较

#### 方法一：

&emsp;&emsp;让该对象的类实现Comparable接口(比较规则)，然后重写compareTo方法，自己来指定比较规则。

在compareTo中的约定：

1.认为左边对象 **大于** 右边对象，返回**正整数**。

2.认为左边对象 **小于** 右边对象，返回**负整数**。

3.认为左边对象 **等于** 右边对象，一定返回**零**。

#### 方法二：

&emsp;&emsp;使用下面这个sort方法，创建Comparator比较器接口的匿名内部类对象，然后自己制定比较规则。**自己制定比较规则时，约定和compareTo中约定一样。**

```java
//对数组进行排序
public static <T> void sort(T[] arr, Comparator <? super T> c);
```

## Lambda & 方法引用

### Lambda

1.Lambda表达式被**用于简化函数式接口的匿名内部类**。

2.函数式接口：有且仅有一个抽象方法的接口。

3.Lambda省略规则：

&emsp;&emsp;3.1.参数类型可以省略不写；

&emsp;&emsp;3.2.如果只有一个参数，参数类型可以省略，同时 **()** 也可以省略。

&emsp;&emsp;3.3.如果Lambda表达式中的方法体代码只有一行代码，可以省略大括号不写，同时要省略封号。此时如果这行代码是 return 语句，也必须去掉 return 不写。

### 方法引用

&emsp;&emsp;用于进一步简化Lambda表达式。

1.静态方法引用：如果某个Lambda表达式里只调用一个静态方法，并且前后参数一致，就可以使用静态方法引用。

2.实例方法引用：如果某个Lambda表达式里只调用一个实例方法，并且前后参数一致，就可以使用实例方法引用。

**3.特定类型的方法引用**：如果某个Lambda表达式里只是调用一个实例方法，如果第一个参数列表中的形参中的第一个参数作为了后面的方法的调用者，并且其余参数作为后面方法的形参，则此时就可以使用特定类型的方法引用。

4.构造器引用：如果某个Lambda表达式里只是在创建对象，并且前后参数一致，就能使用构造器引用。

## 正则表达式

&emsp;&emsp;作用1：用来校验数据格式是否合法。

&emsp;&emsp;作用2：在一段文本中查找满足要求的内容。

String提供了匹配正则表达式的方法：

```java
//判断字符串是否匹配正则表达式，匹配则返回true
public boolean matches(String regex);
//用于检测字符串是否以指定的前缀开始
public boolean startsWith(String prefix);
```

### 书写规则

| [abc] | 只能是a,b或c |\[^abc]|除abc外的任何字符|
| [a-zA-Z] | a到z，A到Z，包括  | [a-d[m-p]] |a到d或m-p|
| [a-z&&[def]] | 二者交集 |[a-z&&\[^bc]]|a-z除了bc|
| [a-z&&\[^m-p]] |a到z除了m到p|·|任何字符(一次一个)|
|\d| 一个数字\[0-9](使用\时需要转义) |\D|非数字[^0-9]|
|\s|一个空白字符|\S|非空白字符\[^\s]|
|\w|[a-zA-Z0-9]|\W|[^\w]一个非单词字符|
|X?|X一次或0次|X\*|X0次或多次|
|X+|X一次或多次|X{n}|X正好n次|
|X{n,}|X至少n次|X{n，m}|X至少n次但不超过m次|

### 分割替换

```java
//1.按照正则表达式匹配的内容进行替换
public String replaceAll(String regex, String newStr);
//2.按照正则表达式匹配的内容进行分割字符串，返回一个字符串数组
public String[] split(String regex);
```

### 爬取信息

&emsp;&emsp;1.定义爬取规则；

&emsp;&emsp;2.将正则表达式封装成一个Pattern对象:

```java
Pattern.compile(regex);
```

&emsp;&emsp;3.通过pattren对象去获取查找内容的匹配对象：

```java
Matcher matcher = pattern.matcher(data);
```

&emsp;&emsp;4.定义while循环开始爬取信息：

```java
while(matcher.find()){
    String str = matcher.group();
    System.out.println(str);
}
```

## 异常

&emsp;&emsp;error：系统级别错误，严重问题。

&emsp;&emsp;Exception：异常，程序出现的问题。

&emsp;&emsp;RuntimeException：运行时异常。

&emsp;&emsp;其他异常：例如：编译时异常(编译阶段就会出现错误提示)。

```mermaid2
graph TB
A(Java.lang.Throwable) --> B(error)
A --> C(Exception)
C --> D(RuntimeException)
C --> E(其他异常)
```

### 自定义异常

&emsp;&emsp;throw：抛出一个异常对象，用在方法内。

&emsp;&emsp;throws：抛出方法内部异常，用在方法上。

#### 运行时异常

&emsp;&emsp;定义一个异常类继承 RuntimeException ，重写构造器，通过 “ throw new 异常类(xxx) ” 来创建异常对象并抛出。

#### 编译时异常

&emsp;&emsp;定义一个异常类继承Exception，，重写构造器，通过 “ throw new 异常类(xxx) ” 来创建异常对象并抛出。

```java
try{
    //在try中抓住异常。
}catch(异常类 对象){
    //若有异常则跳入catch中执行
    对象.printStackTrace();
}
```

### 异常的处理

&emsp;&emsp;1.捕获异常，记录异常并响应合适信息给用户。

&emsp;&emsp;2.捕获异常，尝试修复。

## 集合进阶

未完待续...（2023年11月04日）