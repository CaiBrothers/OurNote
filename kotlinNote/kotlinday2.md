IDE创建project 相当于eclipse里创建工作空间
模块相当于eclipse里的项目

##循环
###普通for循环
	for(a in str (step x)) {
  	 	//不带角标的遍历
	}
####
	for((index,c) in str.withIndex()) {
   		//带角标的遍历
	}

###高级for循环
	str.forEach {
   		println(it)   // 不带角标遍历
	}
####
	str.forEachIndexed {
   		index, c -> println( ...)   //带角标遍历
	}

###break和continue
* break和continue 只能用在普通for循环中, 不能用在foreach中, foreach中只能用return;
* 标签处返回：
	* 标签tag@ 
	* break@tag即跳出循环到tag，一般用在多重循环

###while和do-while 同java


##区间和数组
###区间Range (只能定义正向区间)  
* kotlin区间: （1 到100 , a 到 z）
	* 1..100 闭区间 
	* 1 util 100 [1, 100) 半开半闭区间
* IntRange, CharRange,LongRange是一个类
* 区间遍历

###反向区间 
* val range = 100 downTo 1
* IntProgression： Int反向区间类

###数组 
* 创建方法 ：
	* arrayOf("张三","李四","王五") 
	* 基本数据类型自己的创建方式（例如IntArray(size)，BooleanArray(size)），注意：不能用StringArray创建字符串数组，只能用arrayOf

* 数组元素的修改： 
	* arr[1] = 1
	* arr.set(1, 1)

* 数组元素角标查找（没有找到返回-1）：
	* indexof("张三")  
	* lastIndexOf()
	* indexOfFirst（lambda表达式）使用范围更广
	* indexOfLast（lambda表达式）


##when表达式
when表达式 ， 类似java中的switch（只能传入int, short, byte, char, String, 枚举）

优点：支持区间，支持多条件判断

###简单when表达式
	when(age) {
    	1->......
     	2->.....
     	3-> ......
     	4->.......
	}

####

	when(x) {  
		1,2,3->......
     	4,5,6->.....
     	in 7..10-> ......
    	is Int-> ......   //is相当于instanceof

	}


###不带参数的when表达式
	when{
	    age == 7 -> .....
	    age == 12-> ......
	    age == 15-> .......
	    age in 16..20 ->........
	}

###when表达式的返回值：每个判断的最后一行

	fun todo(age):String {
		return when（age） {
		    7 -> {
		    	println（“....”）
				"开始上小学"
		    }	
			12 -> {
		    	println（“....”）
				"开始上中学"
		    }	
		}
	}

##函数表达式

###函数表达式定义
* 对于函数体只有一行的情况： 可以省略{ } 和return， 用=连接

* fun add (a: Int, b:Int): Int = a + b     返回值也可以省略为 fun add(a: Int, b:Int) = a + b
* fun sayHello(): Unit = println("say hello") 

###函数变量及函数引用(::)
val padd = ::add //获取函数的引用 ，类似于C语言的函数指针
padd(10, 20) 或 padd.invoke(10, 20) 调用 ，padd?.invoke() 可以处理变量为空的情况

在创建函数变量的时候直接定义函数体
val padd:(Int, Int) -> Int = { a: Int , b: Int -> a + b}
padd(10, 20)

###函数默认参数和具名参数（解决java中方法的重载可能造成重载方法过多的问题）
* 正常情况：

		fun sendRequest(path:String, method:String) {
			println("请求路径= 。。。 method = ${method}")
		}
* 优化情况：
	
		fun sendRequest(path:String, method:String = "get" // 默认参数) { 
			println("请求路径= 。。。 method = ${method}")
		}

* 调用时 

		sendrRequest( path = "...." , method = "get")  //具名参数


###可变参数(vararg) ：
	fun add(vararg arr: Int) : Int {
		//将传入的参数对应为数组arr
	}


##异常 
###运行时异常

try..catch..finally 语句和java相同

###编译时异常
* kotlin不检查编译时异常 val file = File(path) 

* 详细阐述：王垠的博客关于kotlin和checkException


##递归和尾递归优化
注意：kotlin中函数传入参数是不可变的，无法进行修改操作

###递归和迭代的优缺点
* 递归
	* 优点：逻辑简单，容易实现   
	* 缺点：容易栈内存溢出
* 迭代
	* 优点：内存开销小     
	* 缺点：抽象出数学模型


###尾递归优化
尾递归：函数在调用自己之后没有执行其他任何操作

尾递归优化操作步骤：

* 将递归转换为尾递归
* 函数用tailrec修饰

原理：在java中转化为迭代


##面向对象
复杂类型可以由基本数据类型组成

###运算符重载
运算符重载：kotlin里面每一个运算符对应的都是一个方法，运算符相当于方法的简写

* 通过运算符重载可以定义对象的加减乘除，自增自减等操作

* 运算符重载的函数需要用operator修饰

例如：

* 加号 ：a.plus(b)
* 减号 ：a.minus(b)


###IDE快捷键

