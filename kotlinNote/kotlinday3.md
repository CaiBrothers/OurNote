
##封装

###访问器和自定义访问器set和get

* 在kotlin中，类中用var和val定义字段时，不加open修饰时，默认为私有，默认在每个字段后生成get和set方法

* 自定义访问器
	* private set 可以私有set方法，不让外部调用
	* 自定义set方法
		
			class Person {
				var name = ""
					private set
				var age = 14
					set(value) {
            			if(value in 1..150) {
                			field = value
            			}
        			}
			}
	* 注意：
		* 用field代替当前需要set的字段，不能用this.age = value  
		* this.age = value相当于调用set方法，会造成递归调用

###构造函数
* 主构函数（两种方法）
	* 直接在定义类的时候传入参数，class Person(name: String, age: Int){ }，用init { }进行初始化

			class Person(name:String, age: Int) {
				var name = ""
				var age = 0
				init{
					this.name = name
					this.age = age
				}
					
			}
	* 直接在定义类的时候传入参数，用var或val修饰
			
			class Person(var name: String, var age: Int)

* 次构函数：

		constructor(name: String, age: Int) : this(name, age)
	注意：
	* this(name,age) 调用主构函数
	* init和次构的执行顺序：次构函数会先执行init，再执行程序体


##继承
###继承的使用  
	open class Father 
	class Son: Father() 

父类要被继承的属性和行为需要加open关键字修饰，不加open默认为final修饰，不可继承和重写


###抽象类abstract class 
* 不用加open也可以继承
* 抽象类里的属性和行为不一定是抽象，可以没有抽象方法和属性

		abstract class Human {
			abstract var color: String
			abstract var language: String 
			abstract fun eat() 
		}

		class ZhHuman: Human() {
			override var color: String = "黄色"
			override var language: String = "中文"
			override fun eat() { ..... }
		}
* 抽象类反映的是事物的本质，只能单继承
* 抽象类也可以继承抽象类


###接口
* 接口反映的是事物的能力，可以多实现
* 和继承类一样用“：”连接

		interface RideBike() 
		
		class XiaoMing: Human(), RideBike() 

* 接口细节（和java不同点）：
	* 接口中字段不能在接口中直接赋值
	* 接口中方法可以直接在接口中创建方法体实现


##多态
###多态的定义
* 本质：同种功能不同表现形式
* 形式：父类引用指向子类对象
* 特点：调用方法时，通过父类接收，执行的是子类的方法

###智能类型转换（Java中向下转型优化）  

前提：父类引用指向子类对象

	var shepHerdDog: Dog = ShepHerdDog()

智能类型转换： 当判断过为对应类型之后，会智能类型转换为子类，使用子类有而父类没有的方法
	
	if(shepHerdDog is ShepHerdDog) { shepHerdDog.herdShep() } 

主动类型转换：as ， 将shepHerdDog 主动转换为ShepHerdDog 
	
	if(shepHerdDog is ShepHerdDog) { 
		var newShepHerdDog = shepHerdDog as ShepHerdDog
	}

##嵌套类和内部类
###嵌套类
嵌套类默认为static ，与外部类不相通

	class Outer {
		class Inner { } 
	}

###内部类 
	class Outer {
		inner class Inner {...} 
	}
* 嵌套类用inner修饰，相当于没有static修饰，与外部类相通，需要依赖外部类对象
* 可以用this 和this标签访问内部类和外部类里的成员变量


		


##泛型
**在某些情况下，参数类型无法确定，可以任意传入时，可以使用泛型（有一些类不属于Any，所以用Any不好）**

###泛型的定义和使用
* 用< T > 定义泛型
* thing: T 使用泛型
	
		class Box<T>(var thing: T) {}
	

###泛型的三种基本用法
* 定义对象的时候使用泛型

		fun main(args: Array<String>) {
		    var thing = "ssk"
		    Box<String>(thing)
	
		}

* 定义子类的时候使用泛型
	
		class FruitBox(thing: Fruit): Box<Fruit>(thing)

* 定义子类的时候还是不知道类型，继续使用泛型

		class NewBox<T>(thing: T):Box<T>(thing)

###泛型函数
	fun <T> parseType(thing : T) {
		when(thing) {
			is Int -> .....
			is String -> .....
			else -> ......	
		}
	}

###泛型上限
	class FruitBox<T: Fruit>(thing: T) : Box<T>(thing)
* T: Fruit 即泛型上限，类似继承的写法，规定thing只能是Fruit类型或Fruit类型的子类
* 泛型上限是泛型优于Any之处

###泛型擦除
定义：获取带泛型的类名时，泛型会被擦除，无法获得

* java中必须通过反射来获取泛型
* kotlin中可以通过reified和inline关键字来获取泛型

	获取泛型步骤：
	
	* 泛型前加reified
	* 在方法前加inline

###泛型类型投射 
* < out T > 代表可以传入T和T的子类
* < in T > 代表可以传入T和T的父类 
###星号投射
< * > 代表可以传入任何类型


###复习反射中获取类名的方法

* 通过对象获取类名c.javaClass.name
* 通过类获取类名 Person::class.java


