##中缀表达式 
* 定义：infix修饰
* 作用（简单易懂）
	* 让程序看起来简单
	* 可以定义操作符让代码简单易懂

* 使用条件：
	* 必须是成员函数或扩展函数
	* 必须只传入一个参数
	* 参数不能是可变参数或默认参数


##设计模式入门

###类委托
	interface WashPower {
		fun wash()
	}
	
* 两种方式：
	* 把能力（例如洗碗）委托给类名代理
		
			class SmallFather: WashPower by BigSon()  //方式一

			class BigSon: WashPower {
				override fun wash() {
					println("洗碗")
				}

			}

	* 构造函数传入对象，把能力委托给对象代理 （接口代理），这种方式可以改变传入对象，扩展性更好

			class SmallFather2(var washPower: WashPower) : WashPower by washPower //方式二


###属性委托
* 定义：将一个类中的字段委托给另一个类代理，另一个类需要有这个属性的setValue和getValue方法 

		class BigHeadSon {
		
		    var money by Mother()
		    
		}
		class Mother {
		    operator fun getValue(bigHeadSon: BigHeadSon, property: KProperty<*>): Int {
		        return sonMoney
		    } //相当于BigHeadSon getValue方法
		
		    operator fun setValue(bigHeadSon: BigHeadSon, property: KProperty<*>, any: Int) {
		
		        sonMoney += any / 2
		
		    } //相当于BigHeadSon setValue方法
		    
		    var sonMoney = 0
				
		}

###by lazy 惰性加载（属性委托的一种）
	val name1: String by lazy { "张三" }

* 作用：知道具体值，用的时候再加载，节约内存空间
* 注意：
	* 字段必须不可变，由val修饰
	* 使用时将by lazy内的值赋值进去，只有第一次调用该属性时调用by lazy内的内容
	* 可以在成员变量后，也可以单独存在（即放在类和方法外）
	* 返回值是最后一行
	* 线程安全（同步）

###lateinit 延迟加载
	lateinit var name: String 
* 用法：字段不确定是什么值，后面可能用的时候才会赋值
* 注意：
	* 必须是var 修饰
	* 可以在成员变量后，也可以单独存在（即放在类和方法外）
	* 定义变量时不确定具体值


###扩展函数（java.util包的替代）

	fun String?.isEmpty(): Boolean {
	    return this == null || this.length == 0
	
	}

* 定义：fun 类名.函数名() {  //  this 代表该类的对象 }
* 调用：该类对象或者该类的子类对象.函数名() 


###单例设计模式
* java中的单例设计模式：
	* 饿汉式
	
			class OneInstance {
	
			    private static OneInstance instance = new OneInstance();
			
			    private OneInstance(){}
			
			    public static OneInstance getOnInstance() {
			        return instance;
			    }
				
			}	

	* 懒汉式


			class OneInstance2 {
	
			    private static OneInstance2 instance2;
			
			    private OneInstance2(){}
			
			    public static OneInstance2 getOnInstance() {
			
			        synchronized (OneInstance2.class) {
			            if(instance2 == null) {
			                instance2 = new OneInstance2();
			                return instance2;
			            }
			            return instance2;
			
			        }
	
	    		}

			}



* kotlin中的单例设计模式：

		object Person {
		    var name = "张三"
		    var age = 23
			
			fun sayHello() {
				println("hello")
			}	  
		}

	* 定义：object 创建类
	* 调用：直接用类名点调用
	* object类中的属性都默认定义为静态，方法不是
	* 由于属性都定义为静态，所以字段较多时比较耗内存，所以在字段不多时使用


###伴生对象（相当于java中的静态）
	class Person{ 
		companion object { // 该代码块的定义的内容相当于静态，可以通过类名.调用 }
	
	}

* 和java一样的单例

		class Person private constructor(){
	
		    var age = 1
		
		    companion object {
		        var name = "ass"
		        val person by lazy { Person() } //惰性加载，只会加载一次，线程安全
		
		    }
	
		}

##面向对象（kotlin中的其他类）
###枚举和枚举加强
* 普通枚举（同java）， WEEK.values() 可以获得WEEK中所有的值

		enum class WEEK {
	    	MONDAY, TUESDAY, WEDSDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
		}
	
* 枚举加强用法

		enum class COLOR(var r: Int, var g: Int, var b: Int){ 
			RED(255, 0 ,0), GREEN(0, 255, 0), BLUE(0, 0, 255)
			
		}


###数据类 data class 
	data class News(var title: String, var content: String, var writer: String)

* 相当于java中的bean包
* 自动生成hashcode、equals、copy、component等方法
* 还可以解构为字段 

		val (one, two, three, four) = News(one: String,two: String,three: String,four: String)


###密封类
* 和枚举类似，密封类封装的是子类

		sealed class Stack {
		    class AStack: Stack()
		    class BStack: Stack()
		    class CStack: Stack()
		    class DStack: Stack()
		    class EStack: Stack()
		
		}

* 枚举类封装的子类只能在该kt文件中定义，即可以在封装类中，也可以在该文件的封装类外，但不能再其他kt文件中