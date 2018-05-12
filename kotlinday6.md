##高阶函数补充

###统计数量的高阶函数
* count(block: (T) -> boolean)

###集合重新组合map和flatMap
* map：集合的重新组合，将集合元素转化成其他元素
* flatMap：和 map函数类似，flatMap如果返回的是集合的集合会将集合打碎，变为元素的集合

		println("--------黑马商店,用户买过的所有商品？--------")

		val list1 = mutableListOf<Product>()
		
		customer.map { it.products } //得到的是List<List<product>>
		customer.flatMap { it.products } // 得到的是List<product> 

##DSL入门

###DSL定义
* DSL(Domain-Specific Language, 领域特定语言) 指的是转注意特定问题领域的计算机语言
* GPL(general purpose language, 通用计算机语言)，例如java，C++，kotlin等

###kotlin代码DSL化
* 目的：让人容易读懂
* 方法：
	* 扩展函数 
	* 中缀调用 
	* 带接收者的函数字面值（高阶函数lambda表达式）


###DSL总结
* DSL只是问题解决方案模型的外部封装，这个模型可能是一个API库，也可能是一个完整的框架
* 没有具体的标准来区分DSL和普通API， DSL代码更易于理解，不仅对于开发人员，对于技术含量较低的人员来说也更易理解

###构建器设计模式
* 思想： 先通过一个三方的类PersonBuilder保存需要的变量， 最终拿到所有的变量字段之后再创建需要的对象（Person）
* 目的： 构建的数据构建完后无法直接修改


###缩小作用域
* 定义作用域

		@Dsl marker
		anovation class MyTag  //定义限制作用域的类

* 使用作用域：在要缩小的类前加@MyTag注解


###DSL目的： 架构师，CTO方向




