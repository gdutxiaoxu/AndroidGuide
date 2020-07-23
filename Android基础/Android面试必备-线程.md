## 前言

最近准备更新 Android 面试必备基础知识系列，有兴趣的可以关注我的微信公众号 **stormjun94**，有更新时，第一时间会在微信公众号上面发布，同时，也会同步在 GitHub 上面更新，如果觉得对你有所帮助的话，请帮忙 star。

[Android 面试必备 - http 与 https 协议](https://blog.csdn.net/gdutxiaoxu/article/details/97885526)

[Android 面试必备 - 计算机网络基本知识（TCP，UDP，Http，https）](https://blog.csdn.net/gdutxiaoxu/article/details/97618598)

[Android 面试必备 - 线程](https://blog.csdn.net/gdutxiaoxu/article/details/98475465)

[Android 面试必备 - JVM 及 类加载机制](https://xujun.blog.csdn.net/article/details/98896053)

[Android 面试必备 - 系统、App、Activity 启动过程](https://xujun.blog.csdn.net/article/details/99006458)


**[Android_interview github 地址](https://github.com/gdutxiaoxu/Android_interview)**


![stormjun94](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMDUwMjAzLWY1MWIxMjk1MDM5N2E0YzU)

---

## java 线程有几种状态

### 一种解释

java thread的运行周期中, 有几种状态, 在 java.lang.Thread.State 中有详细定义和说明:

NEW 状态是指线程刚创建, 尚未启动

RUNNABLE 状态是线程正在正常运行中,

当然可能会有某种耗时计算/IO等待的操作/CPU时间片切换等, 这个状态下发生的等待一般是其他系统资源, 而不是锁, Sleep等

BLOCKED  

这个状态下, 是在多个线程有同步操作的场景, 比如正在等待另一个线程的synchronized 块的执行释放, 或者可重入的 synchronized块里别人调用wait() 方法, 也就是这里是线程在等待进入临界区
WAITING  

这个状态下是指线程拥有了某个锁之后, 调用了他的wait方法, 等待其他线程/锁拥有者调用 notify / notifyAll 一遍该线程可以继续下一步操作, 这里要区分 BLOCKED 和 WATING 的区别, 一个是在临界点外面等待进入, 一个是在理解点里面wait等待别人notify, 线程调用了join方法 join了另外的线程的时候, 也会进入WAITING状态, 等待被他join的线程执行结束

TIMED_WAITING  

这个状态就是有限的(时间限制)的WAITING, 一般出现在调用wait(long), join(long)等情况下, 另外一个线程sleep后, 也会进入TIMED_WAITING状态

TERMINATED 

这个状态下表示 该线程的run方法已经执行完毕了, 基本上就等于死亡了(当时如果线程被持久持有, 可能不会被回收)

### 另外一种解释

https://www.cnblogs.com/barrywxx/p/4343069.html

1. 新建状态（New）：新创建了一个线程对象。
2. 就绪状态（Runnable）：线程对象创建后，其他线程调用了该对象的start()方法。该状态的线程位于可运行线程池中，变得可运行，等待获取CPU的使用权。
3. 运行状态（Running）：就绪状态的线程获取了CPU，执行程序代码。
4. 阻塞状态（Blocked）：阻塞状态是线程因为某种原因放弃CPU使用权，暂时停止运行。直到线程进入就绪状态，才有机会转到运行状态。阻塞的情况分三种：
    > （一）、等待阻塞：运行的线程执行wait()方法，JVM会把该线程放入等待池中。
   
    >（二）、同步阻塞：运行的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池中。

    > （三）、其他阻塞：运行的线程执行sleep()或join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。
    
5. 死亡状态（Dead）：线程执行完了或者因异常退出了run()方法，该线程结束生命周期。


---



## Java中的锁分类

在读很多并发文章中，会提及各种各样锁如公平锁，乐观锁等等，这篇文章介绍各种锁的分类。介绍的内容如下：

- 公平锁/非公平锁
- 可重入锁（已经获得了锁，再次尝试获取该锁，可以直接获得）
- 独享锁/共享锁
- 互斥锁/读写锁
- 乐观锁/悲观锁
- 分段锁
- 偏向锁/轻量级锁/重量级锁
- 自旋锁
- 

上面是很多锁的名词，这些分类并不是全是指锁的状态，有的指锁的特性，有的指锁的设计，下面总结的内容是对每个锁的名词进行一定的解释。


##  java  中锁的类型

公平锁/非公平锁

公平锁是指多个线程按照申请锁的顺序来获取锁。
非公平锁是指多个线程获取锁的顺序并不是按照申请锁的顺序，有可能后申请的线程比先申请的线程优先获取锁。有可能，会造成优先级反转或者饥饿现象。
对于Java ReentrantLock而言，通过构造函数指定该锁是否是公平锁，默认是非公平锁。非公平锁的优点在于吞吐量比公平锁大。
对于Synchronized而言，也是一种非公平锁。由于其并不像ReentrantLock是通过AQS的来实现线程调度，所以并没有任何办法使其变成公平锁。

可重入锁

可重入锁又名递归锁，是指在同一个线程在外层方法获取锁的时候，在进入内层方法会自动获取锁。说的有点抽象，下面会有一个代码的示例。
对于 Java ReentrantLock而言, 他的名字就可以看出是一个可重入锁，其名字是 Reentrant Lock重新进入锁。
对于Synchronized而言,也是一个可重入锁。可重入锁的一个好处是可一定程度避免死锁。


```
synchronized void setA() throws Exception{
    Thread.sleep(1000);
    setB();
}

synchronized void setB() throws Exception{
    Thread.sleep(1000);
}
```

上面的代码就是一个可重入锁的一个特点，如果不是可重入锁的话，setB可能不会被当前线程执行，可能造成死锁。



[Java中的锁分类](https://www.cnblogs.com/qifengshi/p/6831055.html)

- 独享锁/共享锁

独享锁是指该锁一次只能被一个线程所持有。
共享锁是指该锁可被多个线程所持有。

对于Java ReentrantLock而言，其是独享锁。但是对于Lock的另一个实现类ReadWriteLock，其读锁是共享锁，其写锁是独享锁。
读锁的共享锁可保证并发读是非常高效的，读写，写读 ，写写的过程是互斥的。
独享锁与共享锁也是通过AQS来实现的，通过实现不同的方法，来实现独享或者共享。
对于Synchronized而言，当然是独享锁。

- 互斥锁/读写锁
 
上面讲的独享锁/共享锁就是一种广义的说法，互斥锁/读写锁就是具体的实现。
互斥锁在Java中的具体实现就是ReentrantLock
读写锁在Java中的具体实现就是ReadWriteLock  

[深入理解读写锁—ReadWriteLock源码分析](https://blog.csdn.net/qq_19431333/article/details/70568478)

- 乐观锁/悲观锁

乐观锁与悲观锁不是指具体的什么类型的锁，而是指看待并发同步的角度。
悲观锁认为对于同一个数据的并发操作，一定是会发生修改的，哪怕没有修改，也会认为修改。因此对于同一个数据的并发操作，悲观锁采取加锁的形式。悲观的认为，不加锁的并发操作一定会出问题。
乐观锁则认为对于同一个数据的并发操作，是不会发生修改的。在更新数据的时候，会采用尝试更新，不断重新的方式更新数据。乐观的认为，不加锁的并发操作是没有事情的。

从上面的描述我们可以看出，悲观锁适合写操作非常多的场景，乐观锁适合读操作非常多的场景，不加锁会带来大量的性能提升。


悲观锁在Java中的使用，就是利用各种锁。
乐观锁在Java中的使用，是无锁编程，常常采用的是CAS算法，典型的例子就是原子类，通过CAS自旋实现原子操作的更新。

- 分段锁

分段锁其实是一种锁的设计，并不是具体的一种锁，对于ConcurrentHashMap而言，其并发的实现就是通过分段锁的形式来实现高效的并发操作。
我们以ConcurrentHashMap来说一下分段锁的含义以及设计思想，ConcurrentHashMap中的分段锁称为Segment，它即类似于HashMap（JDK7与JDK8中HashMap的实现）的结构，即内部拥有一个Entry数组，数组中的每个元素又是一个链表；同时又是一个ReentrantLock（Segment继承了ReentrantLock)。
当需要put元素的时候，并不是对整个hashmap进行加锁，而是先通过hashcode来知道他要放在那一个分段中，然后对这个分段进行加锁，所以当多线程put的时候，只要不是放在一个分段中，就实现了真正的并行的插入。
但是，在统计size的时候，可就是获取hashmap全局信息的时候，就需要获取所有的分段锁才能统计。
分段锁的设计目的是细化锁的粒度，当操作不需要更新整个数组的时候，就仅仅针对数组中的一项进行加锁操作。

- 偏向锁/轻量级锁/重量级锁


这三种锁是指锁的状态，并且是针对Synchronized。在Java 5通过引入锁升级的机制来实现高效Synchronized。这三种锁的状态是通过对象监视器在对象头中的字段来表明的。
偏向锁是指一段同步代码一直被一个线程所访问，那么该线程会自动获取锁。降低获取锁的代价。
轻量级锁是指当锁是偏向锁的时候，被另一个线程所访问，偏向锁就会升级为轻量级锁，其他线程会通过自旋的形式尝试获取锁，不会阻塞，提高性能。
重量级锁是指当锁为轻量级锁的时候，另一个线程虽然是自旋，但自旋不会一直持续下去，当自旋一定次数的时候，还没有获取到锁，就会进入阻塞，该锁膨胀为重量级锁。重量级锁会让其他申请的线程进入阻塞，性能降低。

- 自旋锁

在Java中，自旋锁是指尝试获取锁的线程不会立即阻塞，而是采用循环的方式去尝试获取锁，这样的好处是减少线程上下文切换的消耗，缺点是循环会消耗CPU。
典型的自旋锁实现的例子，可以参考自旋锁的实现

[java锁的种类以及辨析（一）：自旋锁](http://ifeve.com/java_lock_see1/)


```
public class SpinLock {

  private AtomicReference<Thread> sign =new AtomicReference<>();

  public void lock(){
    Thread current = Thread.currentThread();
    while(!sign .compareAndSet(null, current)){
    }
  }

  public void unlock (){
    Thread current = Thread.currentThread();
    sign .compareAndSet(current, null);
  }
}
```



---

##  死锁

比如说两个线程，因为锁造成互相等待。具体来说， A,B 线程需要锁住 a,b 变量，但是因为 A 线程锁住了 a 变量，而 b 变量被 B 线程锁住了，导致无法获得 b 变量的锁，而  B 线程需要锁住 a 变量，造成互相等待。

```
import java.util.Date;
 
public class LockTest {
   public static String obj1 = "obj1";
   public static String obj2 = "obj2";
   public static void main(String[] args) {
      LockA la = new LockA();
      new Thread(la).start();
      LockB lb = new LockB();
      new Thread(lb).start();
   }
}
class LockA implements Runnable{
   public void run() {
      try {
         System.out.println(new Date().toString() + " LockA 开始执行");
         while(true){
            synchronized (LockTest.obj1) {
               System.out.println(new Date().toString() + " LockA 锁住 obj1");
               Thread.sleep(3000); // 此处等待是给B能锁住机会
               synchronized (LockTest.obj2) {
                  System.out.println(new Date().toString() + " LockA 锁住 obj2");
                  Thread.sleep(60 * 1000); // 为测试，占用了就不放
               }
            }
         }
      } catch (Exception e) {
         e.printStackTrace();
      }
   }
}
class LockB implements Runnable{
   public void run() {
      try {
         System.out.println(new Date().toString() + " LockB 开始执行");
         while(true){
            synchronized (LockTest.obj2) {
               System.out.println(new Date().toString() + " LockB 锁住 obj2");
               Thread.sleep(3000); // 此处等待是给A能锁住机会
               synchronized (LockTest.obj1) {
                  System.out.println(new Date().toString() + " LockB 锁住 obj1");
                  Thread.sleep(60 * 1000); // 为测试，占用了就不放
               }
            }
         }
      } catch (Exception e) {
         e.printStackTrace();
      }
   }
}
```

---




## java  生产者消费者

[生产者/消费者问题的多种Java实现方式](https://blog.csdn.net/MONKEY_D_MENG/article/details/6251879)


wait() / nofity()方法是基类Object的两个方法，也就意味着所有Java类都会拥有这两个方法，这样，我们就可以为任何对象实现同步机制。

wait()方法：当缓冲区已满/空时，生产者/消费者线程停止自己的执行，放弃锁，使自己处于等等状态，让其他线程执行。

notify()方法：当生产者/消费者向缓冲区放入/取出一个产品时，向其他等待的线程发出可执行的通知，同时放弃锁，使自己处于等待状态。

光看文字可能不太好理解，咱来段代码就明白了：



```
import java.util.LinkedList;  
  
/** 
 * 仓库类Storage实现缓冲区 
 *  
 * Email:530025983@qq.com 
 *  
 * @author MONKEY.D.MENG 2011-03-15 
 *  
 */  
public class Storage  
{  
    // 仓库最大存储量  
    private final int MAX_SIZE = 100;  
  
    // 仓库存储的载体  
    private LinkedList<Object> list = new LinkedList<Object>();  
  
    // 生产num个产品  
    public void produce(int num)  
    {  
        // 同步代码段  
        synchronized (list)  
        {  
            // 如果仓库剩余容量不足  
            while (list.size() + num > MAX_SIZE)  
            {  
                System.out.println("【要生产的产品数量】:" + num + "/t【库存量】:"  
                        + list.size() + "/t暂时不能执行生产任务!");  
                try  
                {  
                    // 由于条件不满足，生产阻塞  
                    list.wait();  
                }  
                catch (InterruptedException e)  
                {  
                    e.printStackTrace();  
                }  
            }  
  
            // 生产条件满足情况下，生产num个产品  
            for (int i = 1; i <= num; ++i)  
            {  
                list.add(new Object());  
            }  
  
            System.out.println("【已经生产产品数】:" + num + "/t【现仓储量为】:" + list.size());  
  
            list.notifyAll();  
        }  
    }  
  
    // 消费num个产品  
    public void consume(int num)  
    {  
        // 同步代码段  
        synchronized (list)  
        {  
            // 如果仓库存储量不足  
            while (list.size() < num)  
            {  
                System.out.println("【要消费的产品数量】:" + num + "/t【库存量】:"  
                        + list.size() + "/t暂时不能执行生产任务!");  
                try  
                {  
                    // 由于条件不满足，消费阻塞  
                    list.wait();  
                }  
                catch (InterruptedException e)  
                {  
                    e.printStackTrace();  
                }  
            }  
  
            // 消费条件满足情况下，消费num个产品  
            for (int i = 1; i <= num; ++i)  
            {  
                list.remove();  
            }  
  
            System.out.println("【已经消费产品数】:" + num + "/t【现仓储量为】:" + list.size());  
  
            list.notifyAll();  
        }  
    }  
  
    // get/set方法  
    public LinkedList<Object> getList()  
    {  
        return list;  
    }  
  
    public void setList(LinkedList<Object> list)  
    {  
        this.list = list;  
    }  
  
    public int getMAX_SIZE()  
    {  
        return MAX_SIZE;  
    }  
}  
/** 
 * 生产者类Producer继承线程类Thread 
 *  
 * Email:530025983@qq.com 
 *  
 * @author MONKEY.D.MENG 2011-03-15 
 *  
 */  
public class Producer extends Thread  
{  
    // 每次生产的产品数量  
    private int num;  
  
    // 所在放置的仓库  
    private Storage storage;  
  
    // 构造函数，设置仓库  
    public Producer(Storage storage)  
    {  
        this.storage = storage;  
    }  
  
    // 线程run函数  
    public void run()  
    {  
        produce(num);  
    }  
  
    // 调用仓库Storage的生产函数  
    public void produce(int num)  
    {  
        storage.produce(num);  
    }  
  
    // get/set方法  
    public int getNum()  
    {  
        return num;  
    }  
  
    public void setNum(int num)  
    {  
        this.num = num;  
    }  
  
    public Storage getStorage()  
    {  
        return storage;  
    }  
  
    public void setStorage(Storage storage)  
    {  
        this.storage = storage;  
    }  
}  
/** 
 * 消费者类Consumer继承线程类Thread 
 *  
 * Email:530025983@qq.com 
 *  
 * @author MONKEY.D.MENG 2011-03-15 
 *  
 */  
public class Consumer extends Thread  
{  
    // 每次消费的产品数量  
    private int num;  
  
    // 所在放置的仓库  
    private Storage storage;  
  
    // 构造函数，设置仓库  
    public Consumer(Storage storage)  
    {  
        this.storage = storage;  
    }  
  
    // 线程run函数  
    public void run()  
    {  
        consume(num);  
    }  
  
    // 调用仓库Storage的生产函数  
    public void consume(int num)  
    {  
        storage.consume(num);  
    }  
  
    // get/set方法  
    public int getNum()  
    {  
        return num;  
    }  
  
    public void setNum(int num)  
    {  
        this.num = num;  
    }  
  
    public Storage getStorage()  
    {  
        return storage;  
    }  
  
    public void setStorage(Storage storage)  
    {  
        this.storage = storage;  
    }  
}  
/** 
 * 测试类Test 
 *  
 * Email:530025983@qq.com 
 *  
 * @author MONKEY.D.MENG 2011-03-15 
 *  
 */  
public class Test  
{  
    public static void main(String[] args)  
    {  
        // 仓库对象  
        Storage storage = new Storage();  
  
        // 生产者对象  
        Producer p1 = new Producer(storage);  
        Producer p2 = new Producer(storage);  
        Producer p3 = new Producer(storage);  
        Producer p4 = new Producer(storage);  
        Producer p5 = new Producer(storage);  
        Producer p6 = new Producer(storage);  
        Producer p7 = new Producer(storage);  
  
        // 消费者对象  
        Consumer c1 = new Consumer(storage);  
        Consumer c2 = new Consumer(storage);  
        Consumer c3 = new Consumer(storage);  
  
        // 设置生产者产品生产数量  
        p1.setNum(10);  
        p2.setNum(10);  
        p3.setNum(10);  
        p4.setNum(10);  
        p5.setNum(10);  
        p6.setNum(10);  
        p7.setNum(80);  
  
        // 设置消费者产品消费数量  
        c1.setNum(50);  
        c2.setNum(20);  
        c3.setNum(30);  
  
        // 线程开始执行  
        c1.start();  
        c2.start();  
        c3.start();  
        p1.start();  
        p2.start();  
        p3.start();  
        p4.start();  
        p5.start();  
        p6.start();  
        p7.start();  
    }  
}  
```

在JDK5.0之后，Java提供了更加健壮的线程处理机制，包括同步、锁定、线程池等，它们可以实现更细粒度的线程控制。await()和signal()就是其中用来做同步的两种方法，它们的功能基本上和wait() / nofity()相同，完全可以取代它们，但是它们和新引入的锁定机制Lock直接挂钩，具有更大的灵活性。通过在Lock对象上调用newCondition()方法，将条件变量和一个锁对象进行绑定，进而控制并发程序访问竞争资源的安全。下面来看代码：


```
import java.util.LinkedList;  
import java.util.concurrent.locks.Condition;  
import java.util.concurrent.locks.Lock;  
import java.util.concurrent.locks.ReentrantLock;  
  
/** 
 * 仓库类Storage实现缓冲区 
 *  
 * Email:530025983@qq.com 
 *  
 * @author MONKEY.D.MENG 2011-03-15 
 *  
 */  
public class Storage  
{  
    // 仓库最大存储量  
    private final int MAX_SIZE = 100;  
  
    // 仓库存储的载体  
    private LinkedList<Object> list = new LinkedList<Object>();  
  
    // 锁  
    private final Lock lock = new ReentrantLock();  
  
    // 仓库满的条件变量  
    private final Condition full = lock.newCondition();  
  
    // 仓库空的条件变量  
    private final Condition empty = lock.newCondition();  
  
    // 生产num个产品  
    public void produce(int num)  
    {  
        // 获得锁  
        lock.lock();  
  
        // 如果仓库剩余容量不足  
        while (list.size() + num > MAX_SIZE)  
        {  
            System.out.println("【要生产的产品数量】:" + num + "/t【库存量】:" + list.size()  
                    + "/t暂时不能执行生产任务!");  
            try  
            {  
                // 由于条件不满足，生产阻塞  
                full.await();  
            }  
            catch (InterruptedException e)  
            {  
                e.printStackTrace();  
            }  
        }  
  
        // 生产条件满足情况下，生产num个产品  
        for (int i = 1; i <= num; ++i)  
        {  
            list.add(new Object());  
        }  
  
        System.out.println("【已经生产产品数】:" + num + "/t【现仓储量为】:" + list.size());  
  
        // 唤醒其他所有线程  
        full.signalAll();  
        empty.signalAll();  
  
        // 释放锁  
        lock.unlock();  
    }  
  
    // 消费num个产品  
    public void consume(int num)  
    {  
        // 获得锁  
        lock.lock();  
  
        // 如果仓库存储量不足  
        while (list.size() < num)  
        {  
            System.out.println("【要消费的产品数量】:" + num + "/t【库存量】:" + list.size()  
                    + "/t暂时不能执行生产任务!");  
            try  
            {  
                // 由于条件不满足，消费阻塞  
                empty.await();  
            }  
            catch (InterruptedException e)  
            {  
                e.printStackTrace();  
            }  
        }  
  
        // 消费条件满足情况下，消费num个产品  
        for (int i = 1; i <= num; ++i)  
        {  
            list.remove();  
        }  
  
        System.out.println("【已经消费产品数】:" + num + "/t【现仓储量为】:" + list.size());  
  
        // 唤醒其他所有线程  
        full.signalAll();  
        empty.signalAll();  
  
        // 释放锁  
        lock.unlock();  
    }  
  
    // set/get方法  
    public int getMAX_SIZE()  
    {  
        return MAX_SIZE;  
    }  
  
    public LinkedList<Object> getList()  
    {  
        return list;  
    }  
  
    public void setList(LinkedList<Object> list)  
    {  
        this.list = list;  
    }  
}  
```



生产者与消费者模式在 Handler 中的体现

[Android MessageQueue源码分析](https://blog.csdn.net/xxxzhi/article/details/52834439)

[Handler机制与生产者消费者模式](https://www.jianshu.com/p/25a05bf42e05)


---

## 面试常见问题

**1、进程和线程之间有什么不同？**

一个进程是一个独立(self contained)的运行环境，它可以被看作一个程序或者一个应用。而线程是在进程中执行的一个任务。Java运行环境是一个包含了不同的类和程序的单一进程。线程可以被称为轻量级进程。线程需要较少的资源来创建和驻留在进程中，并且可以共享进程中的资源。


**2、用户线程和守护线程有什么区别？**

当我们在Java程序中创建一个线程，它就被称为用户线程。一个守护线程是在后台执行并且不会阻止JVM终止的线程。当没有用户线程在运行的时候，JVM关闭程序并且退出。一个守护线程创建的子线程依然是守护线程。

**3、有哪些不同的线程生命期？**

当我们在Java程序中新建一个线程时，它的状态是New。当我们调用线程的start()方法时，状态被改变为Runnable。线程调度器会为Runnable线程池中的线程分配CPU时间并且讲它们的状态改变为Running。其他的线程状态还有Waiting，Blocked 和Dead。读这篇文章可以了解更多关于线程生命周期的知识。


**4、什么是线程调度器(Thread Scheduler)和时间分片(Time Slicing)？**

线程调度器是一个操作系统服务，它负责为Runnable状态的线程分配CPU时间。一旦我们创建一个线程并启动它，它的执行便依赖于线程调度器的实现。时间分片是指将可用的CPU时间分配给可用的Runnable线程的过程。分配CPU时间可以基于线程优先级或者线程等待的时间。线程调度并不受到Java虚拟机控制，所以由应用程序来控制它是更好的选择（也就是说不要让你的程序依赖于线程的优先级）。

**5、你如何确保main()方法所在的线程是Java程序最后结束的线程？**

我们可以使用Thread类的join()方法来确保所有程序创建的线程在main()方法退出前结束。这里有一篇文章关于Thread类的joint()方法。

**6、为什么线程通信的方法wait(), notify()和notifyAll()被定义在Object类里？**

一个很明显的原因是JAVA提供的锁是对象级的而不是线程级的，每个对象都有锁，通过线程获得。如果线程需要等待某些锁那么调用对象中的wait()方法就有意义了。如果wait()方法定义在Thread类中，线程正在等待的是哪个锁就不明显了。

**7、 为什么wait(), notify()和notifyAll()必须在同步方法或者同步块中被调用？**

当一个线程需要调用对象的wait()方法的时候，这个线程必须拥有该对象的锁，接着它就会释放这个对象锁并进入等待状态直到其他线程调用这个对象上的notify()方法。同样的，当一个线程需要调用对象的notify()方法时，它会释放这个对象的锁，以便其他在等待的线程就可以得到这个对象锁。由于所有的这些方法都需要线程持有对象的锁，这样就只能通过同步来实现，所以他们只能在同步方法或者同步块中被调用。

**8、 为什么Thread类的sleep()和yield()方法是静态的？**

Thread类的sleep()和yield()方法将在当前正在执行的线程上运行。所以在其他处于等待状态的线程上调用这些方法是没有意义的。这就是为什么这些方法是静态的。它们可以在当前正在执行的线程中工作，并避免程序员错误的认为可以在其他非运行线程调用这些方法。

**9、 volatile关键字在Java中有什么作用？**
当我们使用volatile关键字去修饰变量的时候，所以线程都会直接读取该变量并且不缓存它。这就确保了线程读取到的变量是同内存中是一致的。

**10、同步方法和同步块，哪个是更好的选择？**

同步块是更好的选择，因为它不会锁住整个对象（当然你也可以让它锁住整个对象）。同步方法会锁住整个对象，哪怕这个类中有多个不相关联的同步块，这通常会导致他们停止执行并需要等待获得这个对象上的锁。



