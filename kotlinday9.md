### 基础班java线程回顾

**视频源：**02.创建线程的两种方式.avi， 03.通过Thread直接卖票缺点.avi， 04.通过Runnable方式共享线程间数据.avi， 05.线程安全问题解决.avi

**知识点：** 创建线程的两种方式；通过同步数据解决安全问题

**概念：** 

两种创建线程的方式：

1. 通过继承Thread创建线程，重写里面的run方法
2. 通过实现Runnable接口创建，重写里面的run方法

synchronized同步用来解决线程安全问题

**需求：** 

**代码:**

```
//第一种
class MyThread extends Thread {

    public void run() {
    
    }
}

//第二种
class MyRunnable implements Runnable {
  	public void run() {
    
    }
}
```

```
class MyRunnable implements Runnable {

    private int ticket = 100;

    @Override
    public void run() {

        while (true) {

            synchronized (MyRunnable.class) {
                if(ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + "卖出第" + ticket-- + "张票");
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                    
                    }
                } else {
                    break;
                }

            }

        }
    }
}
```



**运行结果**

```
从100到1 无重复
```

**小细节（注意事项）**

```
有数据共享时，用第二种runnable方法完成售票操作（也可以将ticket转为静态解决数据共享）
```

**总结**

两种创建线程的方式：

1. 通过继承Thread创建线程，重写里面的run方法
2. 通过实现Runnable接口创建，重写里面的run方法

线程安全问题的产生原因：

1. 多线程
2. 有共享数据
3. 有多条语句操作共享数据

线程安全问题的解决方法：加synchronized同步锁







### 加入线程，守护线程和线程池

**视频源：**06.线程join.avi， 07.守护线程.avi， 08.线程池.avi

**知识点：** join方法，守护线程和线程池

**概念：** 

加入线程：join() 方法

守护线程：setDaemon(true)方法

线程池：程序启动一个线程的成本是比较高的，而使用线程池可以很好的提高性能，尤其是当程序中要创建大量生命期很短的线程时，更要考虑线程池，在线程池中每一个线程在代码结束后，不会死亡，而是回到线程池成为空闲状态，等到下一个对象调用

**需求：** 

**代码:**

```
public static void main(String[] args) {

	System.out.println("主线程执行");

	MyThread mt = new MyThread();
	mt.start();
	try {
		mt.join();  //等mt线程执行完后再执行主线程
	} catch (InterruptedException e) {
	
	}

	System.out.println("主线程结束");

}
```

```
public static void main(String[] args){

        System.out.println("主线程开始");

        MyThread mt = new MyThread();

        mt.setDaemon(true);  //mt设置为守护线程，主线程结束守护线程直接结束
        mt.start();  

        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
        }
        System.out.println("主线程结束");

}
```

```
class Main {

    public static void main(String[] args){

        ExecutorService executorService = Executors.newFixedThreadPool();  //线程池对象

        MyRunnable mr = new MyRunnable();

        executorService.execute(mr);
        executorService.execute(mr);
        executorService.execute(mr);
        executorService.execute(mr);

    }

}
```



**运行结果**

```

```

**小细节（注意事项）**

守护线程守护的是所有的非守护线程，当所有非守护线程结束后，所有守护线程直接结束

```

```

**总结**

加入线程：join() 方法，可以将线程的并行转化为串行

守护线程：setDaemon(true)方法，可以将线程设置为守护线程，所有的非守护线程结束后，守护线程立即结束

线程池：程序启动一个线程的成本是比较高的，而使用线程池可以很好的提高性能，尤其是当程序中要创建大量生命期很短的线程时，更要考虑线程池，在线程池中每一个线程在代码结束后，不会死亡，而是回到线程池成为空闲状态，等到下一个对象调用







### 协程入门

**视频源：**09.第一个协程启动.avi，10.协程打印数据.avi，12.launch函数的参数和返回值.avi，13.launch函数第一个参数.avi，14.ForkJoinPool的原理.avi，15.协程启动之后的处理.avi

**知识点：** launch函数解析，ForkJoinPool线程池

**概念：** 

launch函数的参数和返回值

launch函数的第一个参数解析

ForkJoinPool本质上为线程池，里面的线程可看做守护线程

**需求：** 

**代码:**

```

```

**运行结果**

```

```

**小细节（注意事项）**

```

```

**总结**

launch函数详解：

三个默认参数，和一个函数参数，返回值是Job

第一个参数context ：协程上下文， 默认赋值为defaultDispatcher ， 在底层等于CommonPool（单例），实现原理是通过ForkJoinPool来实现的，ForkJoinPool本质上是线程池

ForkJoinPool ：普通线程池创建的是用户线程，ForkJoinPool创建的是守护线程

解决守护线程问题方法：

1. 主线程sleep   
2. job.join() 将协程加入到主线程







### 协程原理

**视频源：**17.协程实现原理.avi，18.协程执行原理解析.avi，19.挂起函数.avi

**知识点：**	协程实现原理，挂起函数

**概念：** 

1. 线程阻塞而协程非阻塞
2. 协程通过挂起执行并行
3. 挂起函数：suspend修饰的函数；只有挂起函数可以被挂起

**需求：** 

**代码:**

```
fun main(args: Array<String>) = runBlocking {

    //同步和异步， 阻塞和非阻塞

    val job = launch {

        println("协程执行前：${Thread.currentThread().name}")

        delay(2000L)

        println("协程结束：${Thread.currentThread().name}")

    }



    launch {

        Thread.sleep(1000)
    }
    launch {

        Thread.sleep(1000)
    }
    launch {

        Thread.sleep(1000)
    }
    launch {

        Thread.sleep(1000)
    }

    job.join()

}
```

**运行结果**

```
协程执行前：ForkJoinPool.commonPool-worker-1
协程结束：ForkJoinPool.commonPool-worker-2
```

**小细节（注意事项）**

协程通过delay挂起，挂起结束后更换了线程执行，说明原线程没有在挂起时阻塞

```

```

**总结**

协程和线程的比较:

1. 线程是阻塞式，协程是非阻塞式
2. 协程可以把耗时任务先挂起，等时间到了再从线程池中空闲的线程执行
3. 可挂起的任务必须是挂起函数，例如：delay可挂起，Thread.sleep不能被挂起

挂起函数（suspend修饰）
定义：suspend修饰的函数式挂起函数
使用：挂起函数只能在协程中或挂起函数中执行







### 线程和协程效率比较

**视频源：**20.线程和协程效率对比.avi

**知识点：**	线程和协程效率对比

**概念：** 

由实验比较，协程的效率比线程快10倍左右

**需求：** 

**代码:**

```
fun main(args: Array<String>) = runBlocking {

//    val CoroutineList = List(100000) {
//        launch {
//            println("1")
//        }
//
//    }
//
//    val startTime = System.currentTimeMillis()
//
//    CoroutineList.forEach {
//        it.join()
//    }
//
//    val endTime = System.currentTimeMillis()
//
//    println("协程运行时间 = ${endTime - startTime}")  //协程运行时间928ms


    val threadList = List(100000) {
        MyThread()

    }


    val startTime = System.currentTimeMillis()

    threadList.forEach {
        it.start()
    }

    threadList.forEach {
        it.join()
    }

    val endTime = System.currentTimeMillis()

    println("协程运行时间 = ${endTime - startTime}")  // 线程运行时间11684ms


}


class MyThread: Thread() {
    override fun run() {
        println("2")
    }

}
```

**运行结果**

```
协程运行时间 = 928(ms)
线程运行时间 = 11684(ms)
```

**小细节（注意事项）**

```

```

**总结**

由案例比较，创建100000个线程和协程分别执行时，协程的效率比线程快10倍左右







### 协程的取消方法

**视频源：**21.协程取消.avi，22.协程取消失效.avi，23.协程取消失效的处理.avi

**知识点：**	协程的取消和取消失效

**概念：** 

协程取消：job.cancel() 直接取消， withTimeOut() 定时取消 

取消失效：直接调用cancel只能取消被挂起的函数，不能取消通过Thread.sleep()阻塞的函数

协程取消失效的处理：通过isActive判断线程的状态，通过线程的状态来取消阻塞的函数

**需求：** 

**代码:**

```
fun main(args: Array<String>) = runBlocking {

    val job = launch {
        (1..10).forEach {
            println(it)
            delay(200)
        }

    }

    delay(1000)
    job.cancel()

    job.join()

}
```

**运行结果**

```
1
2
3
4
5
```

**小细节（注意事项）**

cancel要在join前面

```

```

**总结**

协程取消：job.cancel() 直接取消， withTimeOut() 定时取消 

取消失效：直接调用cancel只能取消被挂起的函数，不能取消通过Thread.sleep()阻塞的函数

协程取消失效的处理：通过isActive判断线程的状态，通过线程的状态来取消阻塞的函数







### 协程的取消方法

**视频源：**21.协程取消.avi，22.协程取消失效.avi，23.协程取消失效的处理.avi

**知识点：**	协程的取消和取消失效

**概念：** 

协程取消：job.cancel() 直接取消， withTimeOut() 定时取消 

取消失效：直接调用cancel只能取消被挂起的函数，不能取消通过Thread.sleep()阻塞的函数

协程取消失效的处理：通过isActive判断线程的状态，通过线程的状态来取消阻塞的函数

**需求：** 

**代码：**

```
fun main(args: Array<String>) = runBlocking {

    val job = launch {
        (1..10).forEach {
            println(it)
            delay(200)
        }

    }

    delay(1000)
    job.cancel()

    job.join()

}
```

```
fun main(args: Array<String>) = runBlocking {

    val job = launch {


        withTimeout(1000L) {
            (1..10).forEach {
                println(it)
                delay(200L)
            }

        }

    }

    job.join()

}
```



**运行结果**

```
1   1
2   2
3   3
4   4
5   5
```



**小细节（注意事项）**

cancel要在join前面

```

```

**总结**

协程取消：job.cancel() 直接取消， withTimeOut() 定时取消 

取消失效：直接调用cancel只能取消被挂起的函数，不能取消通过Thread.sleep()阻塞的函数

协程取消失效的处理：通过isActive判断线程的状态，通过线程的状态来取消阻塞的函数







### 协程async启动

**视频源：**24.协程async启动.avi

**知识点：**	协程async启动

**概念：** 

通过async函数启动协程可以获得协程的返回值

**需求：** 

**代码：**

```
fun main(args: Array<String>) = runBlocking{

    /*---------------------------- 有返回值的协程async ----------------------------*/
    val job1 = async { 
    	job1() 
    }
    
    val job2 = async { 
    	job2() 
    }

    val result1 = job1.await()
    val result2 = job2.await()

    println(result1 + result2)

    job1.join()
    job2.join()

}


suspend fun job1(): String {

    println("开始执行job1")
    delay(1000L)
    println("结束执行")
    return "job1"

}

suspend fun job2(): String {

    println("开始执行job2")
    delay(1000L)
    println("结束执行")
    return "job2"

}
```



**运行结果**

```
开始执行job1
开始执行job2
结束执行
结束执行
job1job2
```



**小细节（注意事项）**

```
await()方法是等待协程的返回值
```

**总结**

通过async函数启动协程可以获得协程的返回值







### 协程上下文

**视频源：**25.协程上下文指定.avi

**知识点：** 协程上下文解释

**概念：** 

协程上下文：指定协程代码在哪个线程池中运行

Unconfined：无限制运行在主线程中

coroutineContext：使用父协程的上下文

CommonPool：默认就是CommonPool

自定义线程池上下文：newFixedThreadPoolContext



**需求：** 

**代码：**

```
fun main(args: Array<String>) = runBlocking {

    println("${Thread.currentThread().name}主线程执行")

    val job = launch {
        println("${Thread.currentThread().name}协程执行1")


    }

    println("111")

    val job1 = launch(CommonPool) {
        println("${Thread.currentThread().name}协程执行")

    }
    val job2 = launch(Unconfined) {
        println("${Thread.currentThread().name}协程执行2")

    }
    val job3 = launch(coroutineContext) {
        println("${Thread.currentThread().name}协程执行3")

    }
    val job4 = launch(newFixedThreadPoolContext(3, "新线程")) {
        println("${Thread.currentThread().name}协程执行4")

    }

    job1.join()
    job2.join()
    job3.join()
    job4.join()

}
```



**运行结果**

```
main主线程执行
ForkJoinPool.commonPool-worker-1协程执行1
ForkJoinPool.commonPool-worker-2协程执行
main协程执行2
新线程-1协程执行4
main协程执行3
```



**小细节（注意事项）**

```

```

**总结**

协程上下文：指定协程代码在哪个线程池中运行

Unconfined：无限制运行在主线程中

coroutineContext：使用父协程的上下文

CommonPool：默认就是CommonPool

自定义线程池上下文：newFixedThreadPoolContext

