### 普通程序员的工作流程

**视频源：**02.原始人的工作方式.avi

**知识点：** 普通程序员的工作流程

**概念：** 手动编译，测试，手动依赖管理，打包，上传服务器

**需求：** 全手动完成

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

无





### 自动化构建工具

**视频源：**03.三种构建工具对比.avi

**知识点：**三种构建工具对比

**概念：** Ant， Maven，Gradle 三种常用的构建工具

**需求：** 无

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

 注意：java中不可以仿造kotlin的写法对集合进行循环遍历，在编写for代码时str无法编译通过

```java

```

**总结**

Ant只能做编译测试，Maven可以做编译测试和依赖管理，Gradle可以做编译测试，依赖管理和DSL自定义扩展任务；Gradle是一个很牛逼的构建工具，可以构建一切可构建的内容





### Gradle简介

**视频源：**04.gradle简介.avi

**知识点：**Gradle介绍

**概念：** Gradle介绍

**需求：** 无

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

Gradle三个特点：

1. 构建一切 
2. 自动化一切
3. 速度更快







### Gradle简介

**视频源：**05.gradle下载和配置.avi

**知识点：**gradle的下载和配置方法

**概念：** 无

**需求：** 无

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

1. gradle 4.0之后的版本才支持kotlin
2. 软件必须安装在非中文非空格目录下

```java

```

**总结**

无





### Gradle项目初始化

**视频源：**06.gradle项目初始化.avi

**知识点：**gradle项目初始化

**概念：** gradle项目初始化

**需求：** 需要联网

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

无





### Gradle打包

**视频源：**07.gradle打包.avi

**知识点：**gradle打包

**概念：** 在gradle中java代码的编译到打包过程

**需求：**

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

无





### 动态语言和静态语言

**视频源：**08.静态语言和动态语言.avi

**知识点：**动态语言和静态语言的区别

**概念：** 动态语言（javascript，python等），静态语言（java，C++，kotlin等）

**需求：** 

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

动态语言根据数据的操作判断数据的类型，静态语言的数据类型是直接定义好的，可以直接判断

动态语言代码怎么写都对，但编译时经常报错





### gradle支持kotlin打包

**视频源：**09.gradle支持kotlin开发.avi

**知识点：**kotlin开发打包流程

**概念：** gradle中kotlin开发打包流程

**需求：**

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

无





### task依赖

**视频源：**12.task依赖.avi

**知识点：**task的依赖管理

**概念：** 大象装冰箱的依赖管理过程（放大象依赖开冰箱门， 关冰箱门依赖放大象）

**需求：**

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

无





### task生命周期

**视频源：**13.task生命周期.avi

**知识点：** task生命周期分为扫描时和运行时生命周期

**概念：** 扫描时生命周期是在程序扫描时执行，运行时生命周期在程序运行时执行，运行时执行代码需要加doFirst		或doLast包裹

**需求：**

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

扫描时生命周期是在程序扫描时执行，运行时生命周期在程序运行时执行，运行时执行代码需要加doFirst		或doLast包裹





### 常见gradle插件

**视频源：**17.常见的插件.avi

**知识点：** 常见gradle插件及三方插件查找使用方法

**概念：** 常见gradle插件及三方插件查找使用方法

**需求：** gradle.org中查找三方插件

**代码:**

```kotlin
//三方插件常用调用方式
buildscript {
    repositories {
        maven {
            setUrl("https://plugins.gradle.org/m2/")
        }
    }
    dependencies {
        classpath("org.jetbrains.kotlin:kotlin-gradle-plugin:1.2.41")
    }
}

apply {
    plugin("org.jetbrains.kotlin.jvm")

}

//gradle自带插件的调用方法
plugings {
  application
  java
}
```

**运行结果**

```
无
```

**小细节（注意事项）**

```java

```

**总结**

gradle自带插件通过plugins {} 直接调用， 其他三方插件通过buildScript方法调用

------



### 常见的依赖仓库repositories

**视频源：**24.常见的仓库.avi

**知识点：** 常见的依赖仓库

**概念：** 1. mavenCentral    2. Jcentral     3. 本地local仓库   4. 文件仓库   5. 自定义maven仓库

**需求：** 

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

五种常见依赖仓库

1. mavenCentral   
2. Jcentral     
3. 本地local仓库（即曾经使用过的依赖的cache）  
4. 文件仓库（不推荐使用） 
5. 自定义maven仓库（大公司开发时为了信息私密会将需要的依赖存在本地服务器）





### 依赖的坐标

**视频源：**25.依赖的坐标.avi

**知识点：** 依赖的三要素group， name， version

**概念：** group：用包来命名，表示由哪个组织开发， 相当于人的老家

​	     name：项目名，相当于人的姓名

​	     version：定义jar包的版本， 相当于人的身份证号

**需求：** 

**代码:**

```kotlin
dependencies {
    compile(group = "commons-httpclient", name = "commons-httpclient", version = "3.1")  
}
```

**运行结果**

```

```

**小细节（注意事项）**

```java
dependencies {
    compile("commons-httpclient", "commons-httpclient", "3.1")  //字段名可省略
}
```

**总结**

依赖的三要素group， name， version

调用依赖的方法：在dependencies中调用compile(group = "xxx", name = "bbb", version = "1.0") ， 其中字段名可省略变为 compile("xxx", "bbb", "1.0")





### 依赖的配置阶段

**视频源：**26.依赖的配置阶段.avi

**知识点：** 配置依赖 

**概念：** compile() 配置依赖， testCompile() 配置测试依赖（打包时不会一起打包导出）

**需求：** 

**代码:**

```kotlin
dependencies {
    compile(group = "commons-httpclient", name = "commons-httpclient", version = "3.1")  
}
```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

 compile() 配置依赖， testCompile() 配置测试依赖（打包时不会一起打包导出）







### 依赖冲突

**视频源：**27.版本冲突第一种解决方案.avi ， 28.依赖冲突的解决.avi

**知识点：** 依赖冲突及其解决方案

**概念：** 两个插件依赖同一个依赖的不同版本（version）

解决方案：

1. gradle会自动依赖最高版本的依赖，因为一般情况下高版本依赖兼容低版本依赖 

				    2. 排除依赖性传递
				    3. 强制指定一个版本

**需求：** 

**代码:**

```kotlin
dependencies {

    testCompile("junit", "junit", "4.12") {
        exclude("org.hamcrest")
    }  //配置依赖时排除其中的某个依赖

}

configurations.all {
    resolutionStrategy {
        failOnVersionConflict()
        force("commons-logging:commons-logging:1.0.1")  //发生依赖冲突时强制使用该版本依赖

    }
}

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**

依赖冲突： 两个插件依赖同一个依赖的不同版本（version）

解决方案：

1. gradle会自动依赖最高版本的依赖，因为一般情况下高版本依赖兼容低版本依赖 
2. 排除依赖性传递，就是让gradle不自动依赖，出现冲突时报错，发生错误时可以用exclude("") 强制不导入冲突的依赖 
3. 强制指定一个版本，发生冲突报错时，用force("") 强制指定一个版本







### 分模块开发

**视频源：**29.扩展gradle任务.avi，30.多模块构建简介.avi，31.多模块的依赖.avi，32.多模块构建.avi

**知识点：** 分模块开发

**概念：** 

**需求：** 

**代码:**

```kotlin

```

**运行结果**

```

```

**小细节（注意事项）**

```java

```

**总结**









Gradle
很牛逼的构建工具
构建一切可构建的内容

原始人：
手动编译，测试， 手动依赖管理，打包， 上传至服务器

手动编译：编译为class文件
测试：导入测试工具
导出jar包
写批处理文件.bat上传至服务器

常见构建工具： Ant Maven Gradle

4.1版本

动态语言和静态语言
动态语言（python，groovy，javascript）
静态语言（kotlin，java）

project和task ：
Project是一个接口
gradle构建的时候，首先根据配置文件创建一个Project实例，执行project实例
配置文件中所有代码都会通过task任务的方式插入到project中

application //包含很多常见的任务

task的依赖管理
特点：依赖具有传递性 ，例如a依赖b， b依赖c ，则a也依赖c

task的生命周期
1. 扫描时生命周期： 任务在扫描时执行
2. 执行时生命周期： 任务在执行时执行

如果想让执行不是扫描时的生命周期， 可以用doFirst或doLast


Gradle增量更新 ： 
只更新修改的文件
指定输入源和输出源， inputs.dir() , inputs.file(), outputs.dir(), outputs.file()
用法：只要输入源和输出源不改变，则任务不更新，当输入源和输出源改变时任务更新


插件plugins
系统中的插件plugins { }直接使用

三方公司或个人开发了很多的插件，在官方Gradle网站插件市场中找插件
通过apply { plugin("com.jetbrains.kotlin.jvm")}


gradle的依赖管理
通过gradle自动导入jar包，解决jar包的依赖管理问题

常见仓库
1. mavenCentral（网络仓库）
2. Jcenter（网络仓库）
3. local本地仓库
4. 文件仓库（不建议使用）
   5.自定义maven仓库（最常用）

依赖库的坐标：group ， name ， version

依赖冲突：
1.默认情况下，gradle选择依赖最高版本
2.如果不想让gradle自己解决可以加上
configuration.all { 
	resolutionStrategy {

	}

}


Gradle任务扩展

分模块开发
idea 每一个project相当于工作空间
module相当于eclipse的项目
模块开发时的调用通过compile(project: "Core")

allprojects 构建所有的工程
subprojects 构建子工程
buildscript 构建环境需要用的插件








