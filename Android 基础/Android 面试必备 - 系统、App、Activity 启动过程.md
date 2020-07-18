
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

## Android 系统启动过程



从系统层看：
1. linux 系统层 
2. Android系统服务层 
3. Zygote 

从开机启动到Home Launcher：

1. 启动bootloader （小程序；初始化硬件）
2. 加载系统内核 （先进入实模式代码在进入保护模式代码）
3. 启动init进程（用户级进程 ，进程号为1）
4. 启动Zygote进程（初始化Dalvik VM等）
5. 启动Runtime进程
6. 启动本地服务（system service）
7. 启动 HomeLauncher


### 详细解析

Android系统完整的启动过程，从系统层次角度可分为Linux系统层、Android系统服务层、Zygote进程模型三个阶段；从开机到启动Home Launcher完成具体的任务细节可分为七个步骤，下面就从具体的细节来解读Android系统完整的初始化过程。


一、启动BootLoader


Android 系统是基于Linux操作系统的，所以它最初的启动过程和Linux一样。当设备通电后首先执行BootLoader引导装载器，BootLoader是在操作系统内核运行之前运行的一段小程序。通过这段小程序初始化硬件设备、建立内存空间映射图，从而将系统的软硬件环境引导进入合适的状态，以便为最终调用操作系统内核准备好正确的运行环境。


而Linux系统启动时：

1. 首先要加载BIOS的硬件信息，并获取第一个启动设备的代号
2. 读取第一个启动设备的MBR的引导加载程序（lilo、grub等）的启动信息。
3. 加载核心操作系统的核心信息，核心开始解压缩，并且尝试驱动所有的硬件设备。

 …………

在嵌入式系统中，通常不会有像BIOS那样的固件程序，因此整个系统的加载任务都是通过BootLoader完成的。


二、加载系统内核


Linux内核映像通常包括两部分代码，分别为实模式代码和保护模式代码。当BootLoader装载内核映像到代码段内存时，分别放置实模式代码和保护模式代码到不同的位置，然后进入实模式代码执行，实模式代码执行完成后转入保护模式代码。


实模式和保护模式的概念再次不做过多解释，读者可以自行查阅资料。


三、启动Init进程


当系统内核加载完成之后，会首先启动Init守护进程，它是内核启动的第一个用户级进程，它的进程号总是1。 Init进程启动完成之后，还负责启动其他的一些重要守护进程，包括：

Usbd进程（USB Daemon）：USB连接后台进程，负责管理USB连接。

adbd 进程（Android Debug Bridge Daemon）：ADB连接后台进程，负责管理ADB连接。

debuggerd 进程(Debugger Daemon) ：调试器后台进程，负责管理调试请求及调试过程。

rild进程 (Radio Interface Layer Daemon)： 无线接口层后台进程，负责管理无线通信服务。


四、启动Zygote进程


Init进程和一些重要的守护进程启动完成之后，系统启动Zygote 进程。Zygote 进程启动后，首先初始化一个Dalvik VM实例，然后为它加载资源与系统共享库，并开启Socket监听服务，当收到创建Dalvik VM实例请求时，会通过COW（copy on write）技术最大程度地复用自己，生成一个新的Dalvik VM实例。Dalvik VM实例的创建方法基于linux系统的fork原理。


其实，我个人理解，Zygote进程就相当于Linux系统中的fork进程。由它可以在系统运行期间，接收到创建虚拟机请求时，孵化Dalvik VM实例。Zygote进程孵化Dalvik VM实例流程如下图所示：


![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/1762897_1682.png)


图1  Zygote进程孵化Dalvik VM实例流程


五 、启动Runtime进程


在Zygote进程启动完成之后，Init进程会启动Runtime进程。Runtime进程首先初始化服务管理器（Service Manager），并把它注册为绑定服务（Binder services）的默认上下文管理器，负责绑定服务的注册与查找。然后Runtime进程会向Zygote进程发送启动系统服务（System Service）的请求，Zygote进程收到请求后，会“孵化”出一个新的Dalvik VM实例并启动系统服务进程。Runtime进程的启动流程如下图所示：



![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/1762906_4389.png)


图2  Runtime进程启动流程图


六、启动本地服务


System Service会首先启动两个本地服务（由C或C++编写的native服务），Surface Flinger和Audio Flinger，这两个本地系统服务向服务管理器注册成为IPC服务对象，以便在需要它们的时候很容易查找到。然后SystemService 会启动一些 Android 系统管理服务，包括硬件服务和系统框架核心平台服务，并注册它们成为IPC服务对象。本地服务进程的启动流程如下图所示：


![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/1762920_8157.png)



图3  SystemService启动本地服务流程图


七、启动Home Laucher


当SystemService加载了所有的系统服务后就意味着系统就准备好了，它会向所有服务发送一个系统准备完毕（systemready） 广播。SystemService系统服务进程的启动流程如图1-6所示。当ActivityManagerService 接收到systemready广播后，会向Zygoute进程发送创建Dalvik 虚拟机实例的请求，Zygoute进程会负责生成一个新的Dalvik 虚拟机实例，然后ActivityManagerService在系统中查找具有`<category android:name = "android.intent.category.HOME"/>`属性的Activity，并启动它。ActivityManagerService同时也会使用同样的方法启动Contact（联系人）应用程序。





![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/clipboard.png)


图4  启动Home Laucher流程图

---

## APk  安装过程

### Android应用安装有如下四种方式：

1.系统应用安装――开机时完成，没有安装界面

2.网络下载应用安装――通过market应用完成，没有安装界面

3.ADB工具安装――没有安装界面。

4.第三方应用安装――通过SD卡里的APK文件安装，有安装界面，由         packageinstaller.apk应用处理安装及卸载过程的界面。


### 应用安装的流程及路径  

应用安装涉及到如下几个目录：        

system/app ---------------系统自带的应用程序，获得adb root权限才能删除

data/app  ---------------用户程序安装的目录。安装时把      apk文件复制到此目录 

data/data ---------------存放应用程序的数据 

data/dalvik-cache--------将apk中的dex文件安装到dalvik-cache目录下(dex文件是dalvik虚拟机的可执行文件,其大小约为原始apk文件大小的四分之一)



### 安装过程：

复制APK安装包到data/app目录下，解压并扫描安装包，把dex文件(Dalvik字节码)保存到dalvik-cache目录，并data/data目录下创建对应的应用数据目录。


---

## App 启动过程

这里以启动微信为例子说明

1. Launcher通知AMS 要启动微信了，并且告诉AMS要启动的是哪个页面也就是首页是哪个页面
2. AMS收到消息告诉Launcher知道了，并且把要启动的页面记下来
3. Launcher进入Paused状态，告诉AMS，你去找微信吧

上述就是Launcher和AMS的交互过程

4. AMS检查微信是否已经启动了也就是是否在后台运行，如果是在后台运行就直接启动，如果不是，AMS会在新的进程中创建一个ActivityThread对象，并启动其中的main函数。
5. 微信启动后告诉AMS，启动好了
6. AMS通过之前的记录找出微信的首页，告诉微信应该启动哪个页面
7. 微信按照AMS通知的页面去启动就启动成功了。


---

## Activity 启动过程

Activity 启动过程是由 ActivityMangerService（amS) 来启动的，底层 原理是 Binder实现的 最终交给 ActivityThread 的 performActivity 方法来启动她

ActivityThread大概可以分为以下五个步骤
1. 通过ActivityClientRecoed对象获取Activity的组件信息
2. 通过Instrument的newActivity使用类加载器创建Activity对象
3. 检验Application是否存在，不存在的话，创建一个，保证 只有一个Application
4. 通过ContextImpl和Activity的attach方法来完成一些初始化操作
5. 调用oncreat方法

想详细了解的可以参考这一篇文章，个人觉得写得还不错。[Activity启动过程分析](https://www.jianshu.com/p/13b07beacb1f)

---