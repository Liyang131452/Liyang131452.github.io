---
layout: post
title: 'Maven Notes'
date: 2024-03-20
author: Liyang
cover: 'https://images.unsplash.com/photo-1653629154302-8687b83825e2'
cover_author: 'rogov'
cover_author_link: 'https://unsplash.com/@rogovca'
tags: 
- Java 
- Maven
- Notes 
pin: true
---



## 前言：

&emsp;&emsp;这是一篇关于自学Maven的笔记，用于知识的复习与查找。自学视频：[B站黑马程序员之--Maven](https://www.bilibili.com/video/BV1Ah411S7ZE/?p=1)

如有问题或者不对，请给我发邮件，我进行更正。邮箱：bryceyangli@gmail.com

### 1.Maven简介

#### 1.1.Maven是什么？

​	Maven的本质是一个项目管理工具，将项目开发和管理过程抽象成一个项目对象模型(POM)；

​	POM(Project Object Model)：项目对象模型；

#### 1.2.Maven的作用

​	项目构建：提供标准的、跨平台的自动化项目构建方式。

​	依赖管理：方便快捷的管理项目以来的资源(jar包)，避免资源间的版本冲突问题。

​	统一开发结构：提供标准的、统一的项目结构。

#### 1.3.Maven的下载与配置

​	①[官网下载链接](https://maven.apache.org/download.cgi)

​	②但是如果你要和Idea等工具结合使用，请选择Idea推荐的Maven版本，避免冲突问题。只需将下列网址中的**”3.9.6“**全部更改为自己想要的版本即可下载。

```
https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.zip
```

​	③配置本地仓库：在Maven的**conf**文件夹下的**settings.xml**配置文件中的**50行**附近，将\<localRepository><\localRepository>从注释更改为配置项，在其中复制粘贴自己创建的文件夹路径即可,示例如下;

```
<localRepository>F:\Maven\repository</localRepository>
```

​	④配置镜像仓库：同样在**settings.xml**配置文件的**166行**附近，我使用的是阿里云的镜像仓库，如果你也使用阿里云，可以直接将下列代码拷贝复制到\<mirrors><\mirrors>中

```
    <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>阿里云公共仓库</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
```

​	⑤配置环境变量：将Maven的bin目录(F:\Maven\apache-maven-3.9.5\bin)拷贝添加到环境变量path中，然后使用命令行窗口中输入**”mvn -version**“，出现Maven版本的提时信息即表示环境变量配置成功。

#### 1.4.IDEA配置Maven信息

​	①进入IDEA如下图界面（如果打开默认是项目界面，只要关闭项目（close project）即可），选择**Customize的All settings**，选择Build设置项中的Maven，对Maven home path、User settings file、local repository进行设置，然后点击Apply应用即可。

<img src=".\articleImgs\mavenNotes\1-4-1.png" alt="image-20240324144210284" style="zoom:67%;" />

<img src=".\articleImgs\mavenNotes\1-4-2.png" alt="image-20240324144407957" style="zoom:67%;" />

#### 1.5.仓库

​	用于存储资源，包含各种jar包。[mvnrepository](https://mvnrepository.com)

**仓库分类：**

​	**本地仓库：**自己电脑上存储资源的仓库，连接远程仓库获取资源。

​	**远程仓库：**非本机电脑上的仓库，为本地仓库提供资源。

​			**中央仓库：**Maven团队维护，存储所有资源的仓库。

​			**私服：**部门/公司范围内存储资源的仓库，从中央仓库获取资源。

**私服的作用：**保存具有版权的资源，包含购买或自主研发的jar。一定范围内共享资源，仅对内部开放，不对外共享。

ps：中央仓库中的jar都是开源的，不能存储具有版权的资源。

#### 1.6.坐标

​	Maven中的坐标用于描述仓库中资源的位置。

​	**Maven坐标主要组成：**	

​		groupid：定义当前Maven项目隶属组织名称(通常是域名反写)。 

​		artifactid：定义当前Maven项目名称(通常是模块名称)。

​		version：定义当前项目版本号。

​	**坐标的作用：**使用唯一标识，唯一性定位资源位置，通过该标识可以将资源的识别与下载工作交给机器完成。

###  2.依赖管理

#### 	2.1.依赖配置

依赖指当前项目运行所需的jar，一个项目可以设置多个依赖。

​	格式如下：

```xml
<!--设置当前项目所依赖的所有jar-->
<dependencies>
	<!--设置具体的依赖-->
    <dependency>
        <!--依赖所属群组id-->
        <groupId>junit</groupId>
        <!--依赖所属群组id-->
        <artifactId>junit</artifactId>
        <!--依赖版本号-->
        <version>4.12</version>
    </dependency>
</dependencies>
```

#### 	2.2.依赖传递

依赖具有传递性，且分为直接依赖和间接依赖。

​	**直接依赖：**在当前项目中通过依赖配置建立的依赖关系。

​	**间接依赖：**被依赖的资源如果依赖其他资源，当前项目间接依赖其他资源。	

#### 	2.3.依赖传递冲突问题

​		**路径优先：**当依赖中出现相同的资源时，层级越深，优先级越低，层级越浅，优先级越高。

​		**声明优先：**当资源在相同层级被依赖时，配置顺序靠前的覆盖配置顺序靠后的。

​		**特殊优先：**当同级配置了相同资源的不同版本时，后配置的覆盖先配置的。

#### 	2.4.可选依赖

可选依赖指对外隐藏当前所依赖的资源 ——不透明； 即添加 \<optional>true<\optional>

```xml
 <dependency>
        <!--依赖所属群组id-->
     <groupId>junit</groupId>
        <!--依赖所属群组id-->
     <artifactId>junit</artifactId>
        <!--依赖版本号-->
     <version>4.12</version>
     <optional>true</optional>
</dependency>
```

#### 	2.5.排除依赖

排除依赖指主动断开依赖的资源，被排除的资源无需指定版本——不需要。

```xml
 <dependency>
        <!--依赖所属群组id-->
     <groupId>junit</groupId>
        <!--依赖所属群组id-->
     <artifactId>junit</artifactId>
        <!--依赖版本号-->
     <version>4.12</version>
        <exclusions>
        	<exclusion>
                <groupId>org.hamcrest</groupId>
                <artifactId>hamcrest-core</artifactId>
            </exclusion>
     </exclusions>
</dependency>
```

#### 	2.6.依赖范围：

依赖的jar默认情况可以在任何地方使用，可以通过scope标签设定其作用范围。

​	**作用范围：**主程序范围有效(main文件夹范围内)、测试程序范围有效(test文件夹范围)、是否参与打包(package指令范围内)

|     scope     | 主代码 | 测试代码 | 打包 |    范例     |
| :-----------: | :----: | :------: | :--: | :---------: |
| compile(默认) |   Y    |    Y     |  Y   |    log4j    |
|     test      |        |    Y     |      |    junit    |
|   provided    |   Y    |    Y     |      | servlet-api |
|    runtime    |        |          |  Y   |    jdbc     |

​	**依赖范围传递性：**带有依赖范围的资源在进行传递时，作用范围将受到影响。

|          | compile | test | provided | runtime | 直接依赖 |
| :------: | :-----: | :--: | :------: | :-----: | -------- |
| compile  | compile | test | provided | runtime |          |
|   test   |         |      |          |         |          |
| provided |         |      |          |         |          |
| runtime  | runtime | test | provided | runtime |          |
| 间接依赖 |         |      |          |         |          |

### 3.生命周期与插件

#### 	3.1.项目构建声明周期

Maven构建生命周期描述的是一次构建过程经历了多少个事件。

​	Maven对项目构建的生命周期划分为3套：

​		**clean：清理工作**

​			 pre-clean：执行一些需要在clean之前完成的工作。

​			clean：移除所有上一次构建生成的文件。

​			post-clean：执行一些需要在clean之后立刻完成的工作。

​		**default：核心工作，例如编译，测试，打包，部署等**

​			validate(校验)：校验项目是否正确并且所有必要的信息可以完成项目的构建过程。

​			initialize(初始化)：初始化构建状态，比如设置属性值

​			generate-sources(生成源代码)：生成包含在编译阶段中的任何源代码。

​			process-sources(处理源代码)：处理源代码，比如说，过滤任意值。

​			generate-resources(生成资源文件)：生成将会包含在项目包中的资源文件。

​			process-resources(处理资源文件)：复制和处理资源到目标目录，为打包阶段做好准备。

​			**compile(编译)：编译项目的源代码。**

​			process-classes(处理类文件)：处理编译生成的文件，比如说对Java class 文件做字节码改善优化。

​			 generate-test-sources(生成测试源代码)：生成包含在编译阶段中的任何测试源代码。

​			process-test-sources(处理测试源代码)：处理测试源代码，比如说，过滤任意值。

​			generate-test-resources(生成测试资源文件)：为测试创建资源文件。

​			process-test-resources(处理测试资源文件)：复制和处理测试资源到目标目录。

​			**test-complie(编译测试源码)：编译测试源代码到测试目标目录。**

​			process-test-classes(处理测试类文件)：处理测试源码编译生成的文件。

​			**test(测试)：使用合适的单元测试框架运行测试(Junit是其中之一)。**

​			prepare-package(准备打包)：在实际打包之前，执行任何的必要的操作为打包做准备。

​			**package(打包)：将编译后的代码打包成可分发格式的文件，不如JAR，WAR或者EAR文件。**

​			pre-integration-test(集成测试前)：在执行集成测试前进行必要的动作。比如说，搭建需要的环境。

​			integration-test(集成测试)：处理和部署项目到可以运行集成测试环境中。

​			post-integration-test(集成测试后)：在执行集成测试完成后进行必要的动作。比如说，清理集成测试环境。

​			verify(验证)：运行任意的检查来验证项目包有效且达到质量标准。

​			**install(安装)：安装项目包到本地仓库，这样项目包可以用作其他本地项目的依赖。**

​			deploy(部署)：将最终的项目包复制到远程仓库中与其他开发者和项目共享。

​		**site：产生报告，发布站点等。	**	

​			pre-site：执行一些需要在生成站点文档之前完成的工作。

​			site：	生成项目的站点文档。

​			post-site：执行一些需要在生成站点文档之后完成的工作，并且为部署做准备。

​			site-deploy：将生成的站点文档部署到特定的服务器上。

#### 	3.2插件

​		插件与生命周期内的阶段绑定，在执行到对应生命周期是执行对应的插件功能。

​		默认Maven在各个生命周期上绑定有预设功能。

​		通过插件可以自定义其他功能。

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <version>2.2.1</version>
            <exclusions>
                <exclusion>
                    <goals>
                        <goal>jar</goal>
                    </goals>
                    <phase>generate-test-resources</phase>
                </exclusion>
            </exclusions>
        </plugin>
    </plugins>
</build>
```

### 4.分模块开发与设计

​	将一个完整的项目拆分为多个模块，分模块开发。例如一个项目中包含：controller、dao、pojo、services。

**pojo层：**Plain Ordinary Java Object，也有人称其为model、domain、bean等，pojo层是对应的数据库表的实体类

**持久层：dao层(Mapper)：**Data access object，称为数据访问层。负责与数据库进行联络的一些任务封装在此，具体到对于某个表、某个实体的增删改查。DAO层的设计首先是设计DAO的接口；然后在Spring的配置文件中定义此接口的实现类；然后就可在模块中调用此接口来进行数据业务的处理，而不用关心此接口的具体实现类是哪个类，显得结构非常清晰；DAO层的数据源配置，以及有关数据库连接的参数都在Spring的配置文件中进行配置。

**服务层：Service层：**主要负责业务模块的逻辑应用设计。可以细分为service接口和serviceImpl实现类。首先设计接口，再设计其实现的类；接着再Spring的配置文件中配置其实现的关联。这样我们就可以在应用中调用Service接口来进行业务处理；Service层的业务实现，具体要调用到已定义的DAO层的接口；
封装Service层的业务逻辑有利于通用的业务逻辑的独立性和重复利用性，程序显得非常简洁。service层里面的方法相较于dao层中的方法进行了一层包装，例如通过id查找用户，通过用户名查找用户，是在基础的操作上又增加了一层包装的，实现的是相对高级的操作，最后将这些操作在serviceimpl类中实现。

**表现层：controler层(Handler)**：负责具体的业务模块流程的控制。在此层里面要调用Service层的接口来控制业务流程；控制的配置也同样是在Spring的配置文件里面进行，针对具体的业务流程，会有不同的控制器。

**View层：**此层与控制层结合比较紧密，需要二者结合起来协同工发。View层主要负责前台jsp页面的表示。

**各层之间的联系**：

​	①DAO层，Service层这两个层次都可以单独开发，互相的耦合度很低，完全可以独立进行，这样的一种模式在开发大项目的过程中尤其有优势。

​	②Controller，View层因为耦合度比较高，因而要结合在一起开发，但是也可以看作一个整体独立于前两个层进行开发。这样，在层与层之前我们只需要知道接口的定义，调用接口即可完成所需要的逻辑单元应用，一切显得非常清晰简单。

​	③Service逻辑层设计：Service层是建立在DAO层之上的，建立了DAO层后才可以建立Service层，而Service层又是在Controller层之下的，因而Service层应该既调用DAO层的接口，又要提供接口给Controller层的类来进行调用，它刚好处于一个中间层的位置。每个模型都有一个Service接口，每个接口分别封装各自的业务处理方法。

#### 4.1.pojo拆分

​	①新建模块

​	②拷贝原始项目中对应的相关内容到pojo模块中。

​		**实体类（User）**

​		**配置文件（无）**	

​	因为其中只用到Jdk的核心API，因此直接Cpoy，不用配置xml文件等。

#### 4.2.dao拆分

​	①新建模块

​	②拷贝原始项目中对应的相关内容到dao模块中

​		**数据层接口(UserDao)**

​		**配置文件：**保留与数据层相关配置文件

​			注意：分页插件在配置在与SqlSessionFactoryBean绑定，需要保留。

​		**pom.xml：**引入数据层相关坐标即可，删除springmvc相关坐标

​			spring、mybatis、spring整合mybatis、mysql、durid、pagehelper、直接依赖pojo(对pojo模块执行install命令，将其安装到本地仓库)

#### 4.3.Service拆分

​	①新建模块

​	②拷贝原始项目中对应的相关内容到Service模块中

​		**业务层接口与实现类(UserService、UserServiceImpl)**

​		**配置文件：**保留与数据层相关配置文件

​		**pom.xml：**引入数据层相关坐标即可，删除springmvc相关坐标

​	修改Service模块spring核心配置文件名，添加模块名称，格式：applicationContext-service.xml

​	修改dao模块spring核心配置文件名，添加模块名称，格式：applicationContext-dao.xml

​	修改单元测试引入的配置文件名称，由单个文件修改为多个文件。

#### 4.4.Controller拆分

​	①新建模块

​	②拷贝原始项目中对应的相关内容到controller模块中	

​		**表现层控制器类与相关设置类（UserController、异常相关......）**

​		**配置文件：**保留与表现层相关配置文件、服务器相关配置文件

​		**pom.xml：**引入数据层相关坐标即可，删除springmvc相关坐标

​			spring、springmvc、jackson、servlet、tomcat服务插件、直接依赖service(对service模块执行install命令，将其安装到本地仓库)、间接依赖dao和pojo

​	修改web.xml配置文件中加载spring环境的配置文件名称，使用 * 通配哦，加载所有 applicationContext- 开始的配置文件。

#### 4.5.分模块开发小节

​	模块中仅包含当前模块对应的功能类与配置文件、spring核心配置根据模块功能不同进行独立制作、当前模块所依赖的模块通过导入坐标的形式加入当前模块后才可以使用、web.xml需要加载所有的spring核心配置文件。

### 5.聚合

​	**作用：**聚合用于快速构建maven工程，一次性构建多个项目/模块。

​	**制作方式：**

​		创建一个空没看，打包类型定义为pom

```xml
<packaging>pom</packaging>
```

​		定义当前模块进行构建操作时关联的其他模块名称

```xml
<modules>
    <module>../controller</module>
    <module>../service</module>
    <module>../dao</module>
    <module>../pojo</module>
</modules>
```

注意：参与聚合操作的模块最终执行顺序与模块间的依赖关系有关，与配置顺序无关。

### 6.继承

​	**作用：**通过继承可以实现在子过程中沿用父工程中的配置。

​		maven中的继承与java中的继承相似，在子工程中配置继承关系。

​	**制作方式：**

​		在子工程中声明其父工程坐标与对应的位置

```xml
<!--定义该工程的父工程-->
<parent>
	<groupId>自定义</groupId>
	<artifactId>ssm</artifactId>
	<version>1.0-SNAPSHOT</version>
    <!--填写父工程的pom文件-->
	<relativePath>../ssm/pom.xml</relativePath>
<\parent>
```

​	在父工程中定义依赖管理

```xml
<!--声明此处进行依赖管理-->
<dependencyManagement>
	<!--具体的依赖-->
	<dependencies>
    	<!--spring环境-->
        <dependency>
        	<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.1.9.RELEASE</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

​	在子工程中定义依赖关系，无需声明依赖版本，版本参照父工程中依赖的版本

```xml
<dependencies>
   	<!--spring环境-->
    <dependency>
       	<groupId>org.springframework</groupId>
		<artifactId>spring-context</artifactId>
    </dependency>
</dependencies>
```

#### 继承与聚合

​	**作用：**

​		聚合用于快速构建项目

​		继承用于快速配置

​	**相同点：**

​		聚合与继承的pom.xml文件打包方式均为pom，可以将两种关系制作到同一个pom文件中

​		聚合与继承均属于设计型模块，并无实际的模块内容。

​	**不同点：**

​		聚合是在当前模块中配置关系，聚合可以感知到参与聚合的模块有哪些。

​		继承是在子模块中配置关系，父模块无法感知哪些子模块继承了自己。

### 7.属性

#### 7.1.自定义属性

​	等同于定义变量，方便维护统一。

​	**定义格式：**

```xml
<!--定义自定义属性-->
<properties>
	<spring.version>5.1.9.RELEASE</spring.version>
    <junit.version>4.12</junit.version>
</properties>
```

​	**调用格式：**

```xml
<dependency>
	<groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>${spring.version}</version>
</dependency>
```

#### 7.2.内置属性

​	使用Maven内置属性，快速配置。

​	**调用格式：**

```xml
${basedir}
${version}
```

#### 7.3.Setting属性

​	使用Maven配置文件setting.xml中的标签属性，用于动态配置。

​	**调用格式：**

```xml
${settings.localRepository}
```

#### 7.4.Java系统属性

​	读取Java系统属性。

​	**调用格式：**

```xml
${user.home}
```

​	**系统属性查询方式：**

```cmd
mvn help:system
```

#### 7.5.环境变量属性

​	使用Maven配置文件setting.xml中的标签属性，用于动态配置。

​	**调用格式：**

```xml
${env.JAVA_HOME}
```

​	**环境变量属性查询方式：**

```cmd
mvn help:system
```

### 8.版本管理

#### 8.1.SNAPSHOT

​	项目开发过程中，为方便团队成员合作，解决模块间相互依赖和时时更新的问题，开发者对每个模块进行构建的时候，输出的临时性版本叫快照版本(测试阶段版本)。

​	快照版本会随着开发的进展不断更新。

#### 8.2.RELEASE

​	项目开发到进入阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构件文件是稳定的，即便进行功能的后续开发，也不会改变当前发布版本内容，这种版本称为发布版本。

#### 8.3.版本号约定

​	**约定规范：**

​		<主版本>.<次版本>.<增量版本>.<里程碑版本>

​		**主版本：**表示项目重大架构的变化，如spring5相较于spring4的迭代。

​		**次版本：**表示有较大的功能增加和变化，或者全面系统地修复漏洞。

​		**增量版本：**表示有重大漏洞的修复。

​		**里程碑版本：**表明一个版本的里程碑(版本内部)。这样的版本同下一个正式版本相比，相对来说不是很稳定，有待更多的测试。

​	**示例：**5.1.5.RELEASE

### 9.资源加载属性值

​	在任意配置文件中加载pom文件中定义的属性

**调用格式：**

```xml
${jdbc.url}
```

**开启配置文件加载pom属性：**

```xml
<!--配置资源文件对应的信息-->
<resources>
	<resource>
    	<!--设定配置文件对应的位置目录，支持使用属性动态设定路径-->
        <directory>${project.basedir}/src/main/resources</directory>
        <!--开启对配置文件的资源加载过滤-->
        <filtering>ture</filtering>
    </resource>
</resources>
```

**配置文件中读取pom属性：**

​	在pom文件中设定配置文件路径、开启加载pom属性过滤功能、使用 ${属性名} 格式引用pom属性。

### 10.多环节开发配置

```xml
<!--创建多环境-->
<profiles>
    <!--定义具体的环境：生产环境-->
	<profile>
    	<id>pro_env</id>
        <!--定义环境中专用的属性值-->
        <properties>
        	<jdbc.url>jdbc:mysql://172.1.1.1:3306/db</jdbc.url>
        </properties>
        <!--设置默认启动-->
        <activation>
        	<activeByDefault>ture</activeByDefault>
        </activation>
    </profile>
    <!--定义具体的环境：开发环境-->
	<profile>
    	<id>dev_env</id>
        ...
    </profile>
</profiles>
```

**加载指定环境：**

​	**调用格式：**

```cmd
	mvn 指令 -p 环境定义id
```

​	**范例：**

```cmd
mvn install -p pro_env
```

### 11.跳过测试

#### 11.1.使用命令跳过测试

```cmd
mvn 指令 -p skipTests
```

​	注意：执行的指令声明周期必须包含测试环节。

#### 11.2.IDEA开发工具界面操作跳过测试

<img src=".\articleImgs\mavenNotes\11-2-1.png" alt="image-20240325000645318" style="zoom:67%;" />

#### 11.3.使用配置跳过测试

```xml
<plugin>
	<artifactId>maven-surefire-plugin</artifactId>
    <version>2.22.1</version>
    <configuration>
    	<skipTests>ture</skipTests><!--设置跳过测试-->
        <includes><!--包含指定的测试用例-->
            <include>**/User*Test.java</include>
        </includes>
        <excludes><!--排除指定的测试用例-->
        	<exclude>**/User*TestCase.java</exclude>
        </excludes>
    </configuration>
</plugin>
```

### 12.私服Nexus

#### 12.1Nexus安装、启动与配置

​	emmmmm，暂无，不想更新~~2024年03月25日00点15分
