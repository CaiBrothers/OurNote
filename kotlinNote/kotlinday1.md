#day02：吴通  1035152043

##kotlin入门
###kotlin简介
* 区块链需要web3js 
* kotlin可以智能生成js
* kotlin、scala、groovy都是基于JVM的编程语言
* JETbrains 一家做编译器起家的公司创造

###kotlin优点
* 简洁（数据类，扩展方法，区间）， 相对于java
* **空值安全（针对空值处理的运算符）， java中经常出现空指针异常，需要经常判断排除null情况**
* 100%兼容java、scala
* 函数式编程JDK1.8 lambda表达式
* 协程， 相比于线程更加轻量级，可以开启很多条协程
* DSL领域特定语言，可以更方便的写html等

###kotlin前景
* kotlin script（gradle）.kts
* **java虚拟机应用 web kotlinee， javafx**
* **前端开发 kotlinjs**
* **Android开发（主要应用方向）**
* 支持开发ios，oc，swift
* kotlin Native程序（完全抛弃JVM虚拟机），现在还处于开发阶段

###参考资料: 
深度学习一门语言需要关注以下几点

* **官方文档 kotlinlang.org/docs/reference**
* kotlin源码
* kotlin blog

##数据类型和变量声明
###二进制基础
* **int  4字节  10位数级别**
* byte 1字节  -128~127
* long 8字节  19位数级别
* shor 2字节  -32768~32767
* char 2字节
* float 4字节
* double 8字节
* boolean 1字节

###变量声明

* 声明变量式可以智能类型推断, 一旦确定数据类型后不可变

* kotlin数据类型可以通过to方法进行相互转换,且数据类型不同不能相互赋值(小类型同样不能赋值给大类型)

* 可变变量和不可变变量:
	* var 定义可变变量
	* **val 定义不可变变量**, 类似final, 但java中final修饰的叫常量(编译时常量), val定义的是不可变变量, 可以通过反射改变
	* const val 定义常量

	**项目开发中尽量使用val, 实在不能使用再使用var**

###字符串
* 字符串模板
	* 原样输出字符串 """...""" (保留内容的格式)
	* 字符串中引用变量可以用${引用变量名}

* 字符串API
	* 字符串删除空格 trim() 和 trimMargin(marginPrefix : "|")
	* 字符串的比较 : equals 和 == 等价,  要比较地址值用===
	* 字符串的切割 : split 返回值是字符串集合,  可以多条件切割
	* 字符串的截取 : substring(0, 6)截取第0到第5个字符, substringBefore("r")截取第一个r之前的字符串, substringBeforeLast("r") 截取最后一个r之前的字符串, substringAfter("r") 截取第一个r之后的字符串,substringAfterLast("r") 截取最后一个r之后的字符串

###元组数据
* 二元元组pair, 类似HashMap
* 三元元祖triple

###空值处理(重点)
* val str : String   定义非空类型String
* val str : String? 定义可空类型String?
* str!!  非空断言, 关闭空检查, 不建议使用, 容易造成空指针异常
* str?.toInt()  中  str? 即空安全调用符, 相当于非空判断, 返回的是Int?类型
* **val b: Int = str?.toInt()?: -1    Evis操作符  ?:**

###人机交互
* readLine() 输入内容, 自动将内容转换为字符串
* println()  输出内容	

##函数
###自定义函数
* fun sayHello(){ } 无参无返回, 或者返回值为Unit(相当于java中的void)
* fun sayHello(name:String){ } 有参无返回
* fun getLength(name:String): Int { } 有参有返回
* 无参有返回不列举

###函数式编程: 函数是一等公民, 可以独立于对象单独存在, 闭包
* 顶层函数 : 不是定义在对象内的函数即顶层函数 
* 嵌套函数 : 定义在函数中的函数

##条件控制语句
* kotlin没有三元运算符, 但if语句有返回值可以直接return
* java 声明式语句, kotlin 表达式语句


