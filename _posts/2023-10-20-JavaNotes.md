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
A(Java.lang.Throwable ) --> B(error)
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

&emsp;&emsp;集合被分为单列集合和双列集合两种。单列集合：Collection(每个元素只包含一个值)；双列集合：Map(每个元素包含两个值，形成键值对)。

### Collection集合(单列集合)

```mermaid2
graph TB
A[Collection &#60; E &#62;] --> B[List &#60; E &#62;]
A --> C[Set &#60; E &#62;]
B --> D(ArrayList &#60; E &#62;)
B --> E(LinkedList &#60; E &#62;)
C --> F(HashSet &#60; E &#62;)
C --> G(TreeSet &#60; E &#62;)
F --> H(LinkedHashSet &#60; E &#62;)
```
ps:方角都是接口，圆角都是实现类

**1.Collection集合特点**

&emsp;&emsp;**List集合：**添加的元素是有序、可重复、有索引的。

&emsp;&emsp;**Set系列集合：**添加的元素是无序、不可重复、无索引的。其中LinkedHashSet添加的元素是有序的。TreeSet添加的元素按照大小默认升序排序。

**2.Collection常用方法**

```java
//1.添加元素，添加成功返回true
public boolean add(E e);
//2.清空集合元素
public void clear();
//3.判断集合元素是否为空,若空，则返回true
public boolean isEmpty();
//4.获取集合的大小
public int size();
//5.判断集合中是否包含某元素
public boolean contains(Object obj);
//6.删除某元素，若有多个，默认删除第一个。删除成功返回true
public boolean remove(Object obj);
//7.把集合转为数组
public Object[] toArray();
```

**3.Collection遍历方法**

&emsp;**3.1.迭代器：**用来遍历集合的专用方式。(数组没有)

&emsp;&emsp;Java中迭代器的代表为:Iterator；

&emsp;&emsp;Collection集合获取迭代器的方法：**Iterator\<E> iterator();** 返回集合中的迭代器对象，该迭代器对象默认指向当前集合的第一个元素。

&emsp;&emsp;Iterator中常用方法：

```java
//1.询问当前位置是否有元素存在，若存在则返回true
boolean hasNext();
//2.获取当前位置的元素，并同时将迭代器对象指向下一元素
E next();
```

&emsp;**3.2.增强for循环**:（集合数组都可以）

```java
for(元素的数据类型名 变量名:数组或集合){
    //具体操作
}
//注：增强for循环本质就是迭代器的简化写法
```

&emsp;**3.3.Lambda表达式遍历集合**：

```java
//使用方法
default void forEach(consumer < ? super T> action);//结合Lambda遍历集合
//c.forEach(System.out::println);
```

#### List集合

&emsp;&emsp;插入的数据是有序，可重复，有索引的。

```java
//特有方法：
//1.1.在某个索引位置插入元素
public void add(int index, E element);
//1.2.根据索引删除元素，并返回被删除的元素
public E remove(int index);
//1.3.返回集合中指定位置的元素
public E get(int index);
//1.4.修改索引位置处的元素，修改成功后，会返回原来的数据
public E set(int index, E element);

//遍历方式：未完待续
//2.1.for循环
//2.2.迭代器
//2.3.增强for循环
//2.4.Lambda表达式

//LinkedList集合新增的首尾操作的特有方法
//3.1.新增头元素节点
public void addFirst(E e);
//3.2.新增尾元素节点
public void addLast(E e);
//3.3.获得头节点元素
public E getFirst();
//3.4.获得尾节点元素
public E getLast();
//3.5.删除并返回第一个节点元素
public E removeFirst();
//3.6.删除并返回最后一个节点元素
public E removeLast();
```

#### Set集合

&emsp;&emsp;插入的数据是无序，不重复，无索引的。

注意：`LinkedHashSet`：插入的数据是有序的；`TreeSet`：默认对存入的数据升序排序；相比于Collection集合的常用功能，几乎没有新增常用功能。

**1.HashSet集合的底层原理**

&emsp;&emsp;**1.1.哈希值**：本质是一个`int类型`的数值，Java中每一个对象都有一个哈希值。Java中的对象都可以调用 `Object类 `提供的`hashCode()`方法，并返回对象自己的哈希值。

```java
public int hashCode();
```

&emsp;&emsp;**1.2.特点**：同一对象多次调用`hashCode()`方法返回的哈希值是相同的；不同对象它们的哈希值一般不相同，但也有可能会相同(`int类型`数据有限，因此会发生`哈希碰撞`)。

&emsp;&emsp;**1.3.底层原理**：

$$
基于哈希表实现 =  
\begin{cases}
 JDK8之前:哈希表 = 数组 + 链表  \\
 JDK8之后:哈希表 = 数组 + 链表 + 红黑树
 \end{cases}
$$

**注意**：`哈希表`是一种增删改查数据性能都较好的`数据结构`；如果`链表`的长度 **大于** 8 将会转为`红黑树`；**红黑树**：自动平衡的二叉排序树。

&emsp;&emsp;**1.4.HashSet的去重复机制**：`hashSet集合`默认不能对**内容一样**的两个**不同对象**去重。若想实现不同对象的去重，则需要重写`hashCode()`方法和`equals()`方法。

**2.LinkedHashSet底层原理**

&emsp;&emsp;同样基于`哈希表`，但其每个元素都有额外的**双链表的机制**，双链表记录了它前后元素的位置。

**3.TreeSet集合**

&emsp;&emsp;**3.1.**插入的数据不能重复、且无索引、但是会被自动排序(基于红黑树实现)。

&emsp;&emsp;**3.2.**对于**自定义类型**的对象，TreeSet默认**无法排序**，需要**自定义排序规则**。

&emsp;&emsp;**3.3.自定规则**：①实现`Comparable接口`，重写`CompareTo方法`来指定比较规则；②通过调用**TreeSet集合有参构造器**，可以设置`Comparator对象`。

```java
public TreeSet(Comparator <? super E> comparator);
```

#### 集合的并发修改异常

&emsp;&emsp;使用迭代器自己的方法去修改数据；尤其是`i--`；

emmmmm，标记，记不清楚了。2023年1105。

#### Collection的其他相关知识

&emsp;&emsp;**1.可变参数**：一种特殊类型的形参。定义在构造器、方法的形参列表内。**格式**：`数据类型...参数名称;`。**好处**：常用来灵活的接收数据。**特点**：可以不传数据给它，可以**传一个**或同时**传多个数据**，也可以**传一个数组**给它。

**注意**：一个形参列表中只能有一个可变参数，可变参数必须放在形象列表最后边。

&emsp;&emsp;**2.Collections工具类**：用来操作集合的工具类。

```java
//2.1.给集合批量添加元素
public static <T> boolean addAll(Collection<? super T> c, T...elements);
//2.2.打乱List集合中的元素顺序
public static void shuffle(List<?> list);
//2.3.对List集合中的元素进行升序排序
public static <T> void sort(List<T> lsit);
//2.4.对List集合中元素按照比较器对象指定的规则进行排序
publci static <T> void sort(List<T> list, Comparator<? super T> c);
```

### MAP集合(双列集合)

&emsp;&emsp;**1.MAP集合的体系**

```mermaid2
graph TB
A[Map &#60; k,v &#62;] --> B(HashMap &#60; k,v &#62;)
A --> C(...)
A --> D(TreeMap &#60; k,v &#62;)
B --> E(LinkedHashMap &#60; k,v &#62;)
```

&emsp;&emsp;**2.格式**

`{ key1 = value1, key2 = value2, ... };`一次需要存储一对数据做为一个元素。

&emsp;&emsp;**3.**Map集合的每个元素`“key = value”` 称为一个**键值对/键值对对象/一个Entry对象**，Map集合也被称为**键值对集合**。

&emsp;&emsp;**4.**Map集合的所有**键是不允许重复**的，但**值可以重复**，键和值是一一对应的，每个键只能找到自己对应的值。

&emsp;&emsp;**5.Map集合体系的特点**：**注意**：Map系列集合的特点都是由**键决定**，而**值不做要求**。

`HashMap`：插入的数据是**无序**，**不能重复**、**无索引**的。`LinkedHashMap`：插入的数据是**有序**、**不能重复**、**无索引**的。`TreeMap`：插入的数据按照大小默认**升序排序**，**不能重复**，**无索引**的。

​	**6.经典代码**

```java
Map(String,Integer) map = new HashMap<>();
```

&emsp;&emsp;**7.常用方法**

```java
//1.向集合添加数据
public void put(K key, V value);
//2.获取集合大小
public int size();
//3.清空集合
public void clear();
//4.判断集合是否为空
public boolean isEmpty();
//5.根据键获取对应值
public V get(Object key);
//6.根据键删除整个元素,并返回对应的值
public V remove(Object key);
//7.判断集合是否包含某个键
public boolean containsKey(Object key);
//8.判断是否包含某个值
public boolean containsValue(Object value);
//9.获取Map集合的全部键
public Set<k> keySet();
//10.获取Map集合的全部值
public Collection<v> values();
```

&emsp;&emsp;**8.集合的遍历方式**

**8.1键找值**：先获取Map集合的全部键，再通过遍历键来找值。

```java
public Set<k> keySet();
public V get(Object value);
```

**8.2键值对**：把"键值对"看作一个整体进行遍历。

&emsp;&emsp;①调用Map集合提供的`entrySet`方法，把Map集合转换成键值对类型的Set集合。

```java
Set<Map.Entry<k,v>> entrySet();
```

&emsp;&emsp;②使用`增强for循环`来进行遍历

```java
K getKey();//获取键
V getValue();//获取值
```

**8.3Lambda表达式**(JDK1.8之后新增)

&emsp;&emsp;需要和以下方法结合使用:

```java
default void forEach(BiConsumer<? super K, ? super V> action)//结合Lambda遍历Map
/*
例如：
map.forEach((k,v)->{
	System.out.println(k+"--->"+v);
})
*/
```

**9.HashMap集合的底层原理和应用场景**

&emsp;&emsp;`HashMap`和`HashSet`的底层原理相同，都是基于`哈希表`实现的。

&emsp;&emsp;**实际上：**Set系列集合的底层就是基于Map实现的，只是Set集合中的元素只要键数据，不要值数据。

&emsp;&emsp;**链表长度超过 8 且数组长度大于等于 64 ，底层自动转换为红黑树。**

&emsp;&emsp;`HashMap`的键依赖`HashCode()`和`equals()`保证**键的唯一性**。

&emsp;&emsp;**集合的嵌套**：集合中的元素又是一个集合。







emmmmm,未完待续。最后一次更新：20231106