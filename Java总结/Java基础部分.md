## Java基础部分
### 1. Java跨平台原理
Java通过不同的系统、不同版本、不同位数的Java虚拟机（JVM）来屏蔽不同的系统指令集差异，而对外统一的接口（Java API）。对开发者而言，按照接口开发即可。部署系统则只需要在不同的环境中安装对应版本的虚拟机即可。
### 2. 搭建一个Java开发环境
1. 下载适用开发环境的jdk安装，配置好`JAVA_HOME`，java应用（eclipse、tomcat等）会依赖于这个变量。
2. 下载安装eclipse，设置workspace的默认编码。
3. 下载安装tomcat，把tomcat集成到eclipse中。
4. 安装其他开发插件。

### 3. Java基础类型、占用字节及默认值



| 数据类型 | 大小（二进制位） | 范围             | 默认值 |
| -------- | ---------------- | ---------------- | ------ |
| byte     | 1字节（8bit）    | -128~127         | 0      |
| short    | 2字节（16bit）   | -32768~32767     | 0      |
| int      | 4字节（32bit）   | -2(31) ~ 2(31)-1 | 0      |
| long     | 8字节（64bit）   | -2(31) ~ 2(31)-1 | 0      |
| float    | 4字节（32bit）   | -2(63) ~ 2(63)-1 | 0.0f   |
| double   | 8字节（64bit）   | -2(63) ~ 2(63)-1 | 0.0d   |
| char     | 2字节（16bit）   | \u0000~\uffff    | \u0000 |
| boolean  | 1字节(1bit)      | true/false       | false  |

### 4. 面向对象的特征
面向对象的四大特征：封装、抽象、继承、多态。
- **封装**：将对象封装为一个高度自治和相对封闭的个体，对象状态（属性）由这个对象自己的行为（方法）来读取和改变。
- **抽象**：把现实生活中一些事物相似和共性之处归为一类，忽略和当前主题无关的方面，抽象为类。
- **继承**：把一个已经存在的类所定义的内容作为自己的内容，并且可以加入自己的内容，或者修改原来的方法使之适用于当前特殊的需要。
- **多态**:父类或者接口定义的引用变量可以指向子类或者具体实现类的实例对象，而程序调用的方法在运行期才动态绑定。就是引用变量所指向的具体类型实例对象的方法，也就是内存里正在运行的那个对象的方法，而不是引用变量的类型中定义的方法。

### 5. 装箱与拆箱
- **装箱**：把基本的数据类型转换成对于的包装类型。
- **拆箱**：就是把包装类型转换为基本数据类型。
```java
Integer i=1;//自动装箱，实际编译会调用Integer.valueOf方法来装箱
int j= i;//自动拆箱 实际在编译调用intValue int j = i.intValue();
``` 
- Java是面向对象的语言，而基本数据类型，不具备面向对象的特性。
- **缓存值**：对象缓存，基本数据类型会有对象缓存。
```java
Integer i=1;
Integer j=1;
i==j;//对象相等，是因为存在缓存值对象，所以i、j指向同一个对象
```
### 6. ==和equals方法的区别
- **==** 用来判断两个变量之间的值是否相等，
如果是基本数据类型的变量值直接比较值，引用类型比较要比较对应的引用的内存地址的首地址。
- **equals** 用来比较两个对象是否一样，判断某些特征是否一样，实际上是调用对象的equals方法进行比较。

### 7. String 、StringBuilder、StringBuffer的区别
- 都是用来表示和操作字符串，也就是多个字符的集合的类。
- String 是内容不可变的字符串。底层使用的是一个不可变的字符数组(final char[]);
- StringBuilder、StringBuffer是内容可改变的字符串，底层使用的是可变的字符数组(没有使用final来修饰)。
- 拼接字符串不能使用String进行拼接，要使用StringBuilder、StringBuffer来拼接。因为String会创建很多新对象，StringBuilder、StringBuffer不会。
- StringBuilder是线程不安全的，效率高；
  StringBuffer是线程安全的，效率低，底层有加同步锁。

### 8. Java中的集合
- Java中的集合分为value、key-value（collection Map）两种。
- 存储值分为List和Set
  - List 是有序的，可以重复。
  - Set 是无序的，不可重复的，根据equals和hashcode判断，因此一个对象要存储在Set里面，必须重写equals和hashcode的方法。
- 存储key-value的为Map

### 9. ArrayList与linkedList的区别
- ArrayList底层使用的是数组，linkedList使用的是链表。
  - 数组具有索引，查询特定的元素比较快，而插入和删除元素比较慢（数组在内存中是一块连续内存时，如果插入或删除是需要移动内存的）。
  - 链表不要求内存是连续的，在当前元素下存放上一个或下一个元素的地址，查询时需要从头部开始，一个个的查找，所以查询效率低。插入时不需要移动内存只需要改吧引用指向即可，所以插入或删除效率高。
- 使用场景
  - ArrayList使用在查询比较多，但是插入和删除比较少的情况。
  - linkedList 使用在查询比较少，插入和删除比较多的情况。

### 10. HashMap与HashTable的区别,及ConcurrentHashMap
- 相同点
  - 都可以用来存储key-value的数据
- 不同点
  - HashMap是可以可以把null作为key或value的，而hashtable是不可以的。
  - HashMap是线程不安全的，效率比较高。hashTable是现场安全的，但是效率低。
- ConcurrentHashMap
  > 通过把整个Map分为N个Segment（类似HashTable）,可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。

### 11. 实现一个拷贝文件的工具类，使用字节流还是字符流
拷贝的文件不确定是只包含字符流，有可能包含字节流（图片、声音、影像等),为考虑通用性，要使用字节流。

### 12. 线程的几种实现方式？
1. 实现方式
  - 通过继承Thread的类实现一个线程
  - 通过实现Runnale接口实现一个线程
  - 继承的拓展性不强，Java只支持单继承，如果一个类继承了Thread就不能继承其他的类了。
2. 启动方式
```java
    Thread thread = new Tread(继承Tread的对象或者实现Runnable的对象);
    tread.start();//启动线程使用的start方法，启动以后执行的是run方法。
```

3. 区分线程
```java
    thread.setName("设置一个线程的名称");//在创建线程完成后，都需要设置线程名称。
```

### 13. 线程并发库Executor
Java并发框架java.util.concurrent是JDK5中引入到标准库中的（采用的是Doug Lea的并发库）
#### 13.1. Java通过Executor提供四种线程池，分别为：
- `newCachedThreadPool()`	创建缓存的线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。
- `newFixedThreadPool(int nThreads)`	创建固定数量的线程池，可以控制线程最大并发数，超出的线程会在队列中等待。
- `newScheduledThreadPool()` 创建固定大小的线程池，可以延迟或定时的执行任务。
- `newSingleThreadExecutor()`	创建单个线程，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序（FIFO、UFO、优先级）执行。

#### 13.2. 线程池的作用
- 限定线程的个数，不会导致由于线程过多导致系统运行缓慢或崩溃。
- 线程池不需要每次都去创建或销毁，节约资源。
- 线程池也不需要每次都去创建，响应时间更快。
  

#### 13.3. 线程池的概念与Executors类的应用
- 创建固定大小的线程池
- 创建缓存线程池
- 创建单一线程池(如何实现线程死掉后重新启动?)

```java

public class ThreadPoolTest {

    public static void main(String[] args) {
//        ExecutorService threadPool = Executors.newFixedThreadPool(3); //创建一个固定大小的线程池，线程池中有3个线程可以同时服务
        //缓存线程池 线程池中的线程数是动态变化的，当所有线程处于服务状态时，还有需要被服务的任务，自动增加一个线程进行服务
        //当任务执行完毕，线程处于空闲一段时间，超时后则自动回收销毁线程
//        ExecutorService threadPool = Executors.newCachedThreadPool();  
        //创建一个只有一个线程的线程池，当这个线程挂掉时，可以自动生成一个线程来代替
        //可以解决一个网上很多人问的问题(如何实现线程死掉后重新启动?)
        ExecutorService threadPool = Executors.newSingleThreadExecutor();   
        for(int i = 0;i<10;i++){  //往线程池中扔10个任务
            final int task = i;
            threadPool.execute(new Runnable() {  //往线程池中扔了一个任务
                
                @Override
                public void run() {
                    for(int j = 0;j<10;j++){
                        System.out.println(Thread.currentThread().getName()+" is loop of "+ j + "the task of "+task);
                    }
                }
            });
        }
        System.out.println("all of 10 tasks have committed");
        //上述代码执行完后 没有结束，线程池中有3个线程一直存在，所以程序不会结束
        //可以使用 threadPool.shutdown()
        threadPool.shutdown();  //当线程池中线程执行完所有任务，所有线程处于空闲状态时，干掉所有线程，程序自结束
//        threadPool.shutdownNow();  //立即把池子中所有线程干掉，无论任务是否干完
        
    }
}

```

#### 13.4. 关闭线程池
- shutdown 与 shutdownNow的比较
 
```java

package com.java.juc;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * 一、线程池：提供了一个线程队列，队列中保存着所有等待状态的线程。避免了创建与销毁额外的开销，提高了响应的速度。
 * 
 * 二、线程池的体系结构：
 *     java.util.concurrent.Executor: 负责线程的使用与调度根接口。
 *         |--**ExecutorService 子接口：线程池的主要接口
 *             |--ThreadPoolExecutor 线程池的实现类
 *             |--ScheduledExecutorService 子接口：负责线程的调度
 *                 |--ScheduledThreadPoolExecutor : 继承 ThreadPoolExecutor 实现ScheduledExecutorService
 * 三、工具类：Executors
 *     ExecutorService newFixedThreadPool() :创建固定大小的线程池。
 *     ExecutorService newCachedThreadPool(): 创建无限大小的线程池，线程池中线程数量不固定，可根据需求自动更改。
 *     ExecutorService newSingleThreadPool() : 创建单个线程池，线程池中只有一个线程。
 * 
 *  ScheduledExecutorService newScheduledThreadPool() 创建固定大小的线程池，可以延迟或定时的执行任务。
 *
 */
public class TestThreadPool {
    public static void main(String[] args) {
        //1.创建线程池
        ExecutorService threadPool = Executors.newFixedThreadPool(5);
        ThreadPoolDemo demo = new ThreadPoolDemo();
        
        //2.为线程池中的线程分配任务
        for(int i = 0;i<10;i++){
            threadPool.submit(demo);
        }
        
        //3.关闭线程池
        threadPool.shutdown();  //等待现有线程池中的任务之心完毕，关闭线程池，在等待过程中不接收新的任务
        
        
    }
}

class ThreadPoolDemo implements Runnable{
    private int i = 0;
    @Override
    public void run() {
        while(i <= 100){
            System.out.println(Thread.currentThread().getName() + " : " + i++);
        }
    }
}

```

 

 可以在线程池中放一个Callable任务，并且可以过去到返回结果
```java

package com.java.juc;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

/**
 * 一、线程池：提供了一个线程队列，队列中保存着所有等待状态的线程。避免了创建与销毁额外的开销，提高了响应的速度。
 * 
 * 二、线程池的体系结构：
 *     java.util.concurrent.Executor: 负责线程的使用与调度根接口。
 *         |--**ExecutorService 子接口：线程池的主要接口
 *             |--ThreadPoolExecutor 线程池的实现类
 *             |--ScheduledExecutorService 子接口：负责线程的调度
 *                 |--ScheduledThreadPoolExecutor : 继承 ThreadPoolExecutor 实现ScheduledExecutorService
 * 三、工具类：Executors
 *     ExecutorService newFixedThreadPool() :创建固定大小的线程池。
 *     ExecutorService newCachedThreadPool(): 创建无限大小的线程池，线程池中线程数量不固定，可根据需求自动更改。
 *     ExecutorService newSingleThreadPool() : 创建单个线程池，线程池中只有一个线程。
 * 
 *  ScheduledExecutorService newScheduledThreadPool() 创建固定大小的线程池，可以延迟或定时的执行任务。
 *
 */
public class TestThreadPool {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        //1.创建线程池
        ExecutorService threadPool = Executors.newFixedThreadPool(5);
        ThreadPoolDemo demo = new ThreadPoolDemo();
        
        List<Future> futureList = new ArrayList<>();
        
        for(int i = 0; i<10; i++){
            Future<Integer> future = threadPool.submit(new Callable<Integer>() {
                public Integer call(){
                    int num = 0;
                    for(int i = 0;i<=100;i++){
                        num+=i;
                    }
                    return num;
                }
            });
            futureList.add(future);
        }
        
        for(int i = 0;i<futureList.size();i++){
            System.out.println(futureList.get(i).get());
        }
        
//        //2.为线程池中的线程分配任务
//        for(int i = 0;i<10;i++){
//            threadPool.submit(demo);
//        }
        
        //3.关闭线程池
        threadPool.shutdown();  //等待现有线程池中的任务之心完毕，关闭线程池，在等待过程中不接收新的任务
    }
}

class ThreadPoolDemo implements Runnable{
    private int i = 0;
    @Override
    public void run() {
        while(i <= 100){
            System.out.println(Thread.currentThread().getName() + " : " + i++);
        }
    }
}

```

> 5050
5050
5050
5050
5050
5050
5050
5050
5050
5050

 
#### 13.5. 用线程池启动定时器

- 调用ScheduleExecutorService 的 schedule 方法，返回的ScheduleFuture对象可以取消任务。
- 支持间隔重复任务的定时方式，不直接支持决定定时的方法，需要转换成相对时间方式。
 

 用线程池启动定时器
```java

Executors.newScheduledThreadPool(3).schedule(
                new Runnable() {
                    @Override
                    public void run() {
                        System.out.println("bombing!");
                    }
                }, 
                10, 
                TimeUnit.SECONDS);

```

 

还可以在上述代码中添加固定频率
```java

//固定频率 10秒后触发，每隔两秒后执行一次
        Executors.newScheduledThreadPool(3).scheduleAtFixedRate(
                new Runnable() {
                    @Override
                    public void run() {
                        System.out.println("bombing!");
                    }
                }, 
                10, 
                2,
                TimeUnit.SECONDS);
        //在使用scheduleAtFixedRate 时java api没有提供在某个时间点触发，但API中提示可以通过计算，得到触发的事件点
        // For example, to schedule at a certain future date,
        // you can use: schedule(task, date.getTime() - System.currentTimeMillis(), TimeUnit.MILLISECONDS). 

```

### 14 设计模式
> 设计模式就是经过前人无数次的实践总结出来的，设计过程可以反复使用的、可以解决特定问题的设计方法。

- **单例模式**：某个类只能有一个实例，提供一个全局的访问点。
  - 单例模式有 3 个特点：
    - 单例类只有一个实例对象；
    - 该单例对象必须由单例类自行创建；(饥汉模式是一出来就创建单实例，饱汉模式是需要的时候才创建)；
    - 单例类对外提供一个访问该单例的全局访问点；
  - 饱汉模式（懒汉式）
```java
    public class LazySingleton
{   
    /**
     * 注意：如果编写的是多线程程序，则不要删除代码中的关键字 volatile 和 synchronized，否则将存在线程非安全的问题。
     * 如果不删除这两个关键字就能保证线程安全，但是每次访问时都要同步，会影响性能，且消耗更多的资源，这是懒汉式单例的缺点。
     *
     */
    private static volatile LazySingleton instance=null;    //保证 instance 在所有线程中同步
    private LazySingleton(){}    //private 避免类在外部被实例化
    public static synchronized LazySingleton getInstance()
    {
        //getInstance 方法前加同步
        if(instance==null)
        {
            instance=new LazySingleton();
        }
        return instance;
    }
}
```
  - 饥汉模式（饿汉式）饿汉式--就是穷,不给准备好,担心饿死。类加载就给准备好 
```java
public class HungrySingleton
{   
    /**
    * 饿汉式单例在类创建的同时就已经创建好一个静态的对象供系统使用，以后不再改变，所以是线程安全的，可以直接用于多线程而不会出现问题。
    *
    */
    private static final HungrySingleton instance=new HungrySingleton();
    private HungrySingleton(){}
    public static HungrySingleton getInstance()
    {
        return instance;
    }
}
```
  - 双检锁/双重校验锁（DCL，即 double-checked locking）

    - 是否 Lazy 初始化：
    - 是否多线程安全：是
    - 实现难度：较复杂
    - 描述：这种方式采用双锁机制，安全且在多线程情况下能保持高性能。getInstance() 的性能对应用程序很关键。
    - 代码实例：

```java
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        if (singleton == null) {  
            singleton = new Singleton();  
        }  
        }  
    }  
    return singleton;  
    }  
} 
``` 
- **工厂模式**：Spring IOC使用了工厂模式
  - 对象交给工厂去创建
- **代理模式**：Spring AOP就是使用的动态代理
