



[toc]

>  我的 CSDN 博客:https://blog.csdn.net/gdutxiaoxu <br>
>  我的掘金：https://juejin.im/user/58aa8508570c35006bbd9e03  <br>
>  github: https://github.com/gdutxiaoxu/  <br>
>  微信公众号：徐公码字(stormjun94)  <br>
>  知乎：https://www.zhihu.com/people/xujun94  <br>


## 往期文章


[Android 面试必备 - http 与 https 协议](https://blog.csdn.net/gdutxiaoxu/article/details/97885526)

[Android 面试必备 - 计算机网络基本知识（TCP，UDP，Http，https）](https://blog.csdn.net/gdutxiaoxu/article/details/97618598)

[Android 面试必备 - 线程](https://blog.csdn.net/gdutxiaoxu/article/details/98475465)

[Android 面试必备 - JVM 及 类加载机制](https://xujun.blog.csdn.net/article/details/98896053)

[Android 面试必备 - 系统、App、Activity 启动过程](https://xujun.blog.csdn.net/article/details/99006458)


**[Android_interview github 地址](https://github.com/gdutxiaoxu/Android_interview)**

**有兴趣的话可以关注我的公众号 徐公码字（stormjun94),第一时间会在上面更新**

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/%E5%BE%90%E5%85%AC%E7%A0%81%E5%AD%97%202.jpeg)




## 面试常见

### 一道经典的面试题

还记得这道经典的面试题目吗？从 URL 在浏览器被被输入到页面展现的过程中发生了什么？

总体来说分为以下几个过程:

- DNS 解析:将域名解析成 IP 地址
- TCP 连接：TCP 三次握手
- 发送 HTTP 请求
- 服务器处理请求并返回 HTTP 报文
- 浏览器解析渲染页面
- 断开连接：TCP 四次挥手

完整的可以看以下下面的图片

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/20_04/20200713234113.png)

## http 必备基础知识

HTTP 是一种 超文本传输协议(Hypertext Transfer Protocol)，HTTP 是一个在计算机世界里专门在两点之间传输文字、图片、音频、视频等超文本数据的约定和规范

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/20_07/20200714212848.png)


HTTP 主要内容分为三部分，超文本（Hypertext）、传输（Transfer）、协议（Protocol）。

- 超文本就是不单单只是本文，它还可以传输图片、音频、视频，甚至点击文字或图片能够进行超链接的跳转。
- 上面这些概念可以统称为数据，传输就是数据需要经过一系列的物理介质从一个端系统传送到另外一个端系统的过程。通常我们把传输数据包的一方称为请求方，把接到二进制数据包的一方称为应答方。
- 而协议指的就是是网络中(包括互联网)传递、管理信息的一些规范。如同人与人之间相互交流是需要遵循一定的规矩一样，计算机之间的相互通信需要共同遵守一定的规则，这些规则就称为协议，只不过是网络协议。


### 什么是无状态协议，HTTP 是无状态协议吗，怎么解决

无状态协议(Stateless Protocol) 就是指浏览器对于事务的处理没有记忆能力。举个例子来说就是比如客户请求获得网页之后关闭浏览器，然后再次启动浏览器，登录该网站，但是服务器并不知道客户关闭了一次浏览器。

HTTP 就是一种无状态的协议，他对用户的操作没有记忆能力。可能大多数用户不相信，他可能觉得每次输入用户名和密码登陆一个网站后，下次登陆就不再重新输入用户名和密码了。这其实不是 HTTP 做的事情，起作用的是一个叫做 小甜饼(Cookie) 的机制。它能够让浏览器具有记忆能力。
如果你的浏览器允许 cookie 的话，查看方式 chrome://settings/content/cookies


### 几种方法

HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法

HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT

- GET: 通常用于请求服务器发送某些资源
- HEAD: 请求资源的头部信息, 并且这些头部与 HTTP GET 方法请求时返回的一致. 该请求方法的一个使用场景是在下载一个大文件前先获取其大小再决定是否要下载, 以此可以节约带宽资源
- OPTIONS: 用于获取目的资源所支持的通信选项
- POST: 发送数据给服务器，是**非幂等**的
- PUT: 跟POST方法很像，也是想服务器提交数据。但是，它们之间有不同。PUT指定了资源在服务器上的位置，而POST不需要置顶资源在服务器的位置，是**幂等**的
- DELETE: 用于删除指定的资源
- PATCH: 用于对资源进行部分修改
- CONNECT: HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器
- TRACE: 回显服务器收到的请求，主要用于测试或诊断


### http get 和 post 区别

| Post一般用于更新或者添加资源信息       | Get一般用于查询操作，而且应该是安全和幂等的           |
| ------------- |:-------------:|
| Post更加安全      | Get会把请求的信息放到URL的后面 |
| Post传输量一般无大小限制     | Get不能大于2KB      |
| Post执行效率低 | Get执行效率略高      |




### http put 和 post 区别

**举一个简单的例子**

POST:用于提交请求，可以更新或者创建资源，是非幂等的

举个例子，在我们的支付系统中，一个api的功能是创建收款金额二维码，它和金额相关，每个用户可以有多个二维码，如果连续调用则会创建新的二维码，这个时候就用POST

PUT: 用于向指定的URI传送更新资源，是幂等的

还是那个例子，用户的账户二维码只和用户关联，而且是一一对应的关系，此时这个api就可以用PUT，因为每次调用它，都将刷新用户账户二维码



**如果从 RESTful API 的角度来理解，PUT 方法是这么工作的：**

把一个对象 V 绑定到地址 K 上；今后请求地址 K 时，就会返回对象 V。

如果地址 K 之前曾绑定过另一个对象，比如 V0，那么 V0 会被 V 替换。

举一个简单的例子，假设我的博客后台支持 RESTful API，我可以通过下面的请求发布这篇文章：


```
PUT https://gdutxiao.github.io/2018/04/16/http-put-vs-post HTTP/1.1

{
    /* 文章内容正文 */
}
```

可以看出，使用 PUT 方法时，客户端需要在 HTTP 请求中明确指定地址 K。

正如 Java 的例子一样，PUT 方法应当支持幂等性。如果是同一个对象 V，PUT 多次与 PUT 一次返回的结果应该是相同的。客户端可以利用 PUT 的幂等性安全地重试请求，保证客户端的请求至少被服务端处理一次。

如果把上面发布文章的例子用 HTTP POST 方法重写，它可能会是下面这样：


```
POST https://gdutxiao.github.io/post-article HTTP/1.1

{
    /* 文章内容正文 */
}
```

也就是说，地址 K 不是由客户端指定的，而是由服务端生成的。比如，服务端可能会根据日期和文章标题，为本文分配一个地址。

另外，与 PUT 方法不同，POST 方法是不支持幂等性的。同一个请求被处理两次，应当生成两份对象。换句话说，客户端应该只发送一次 POST 请求，而客户端的请求至多会被服务端处理一次。

> 现在问题来了，如果真的遇到了网络故障，客户端应该如何重试 POST 请求呢？解决方法其实很简单，我们可以在 POST 请求中隐藏一个唯一的 token，服务端在处理请求后把 token 存入数据库，如果这个 token 之前遇到过，服务端就知道这是重复的 POST 请求，可以不再处理了。

## http 版本


### 1.0 与 1.1

- http1.0一次只能处理一个请求，不能同时收发数据
- http1.1可以处理多个请求，能同时收发数据
- http1.1增加可更多字段，如cache-control,keep-alive.

### 2.0

- http 2.0采用二进制的格式传送数据，不再使用文本格式传送数据
- http2.0对消息头采用hpack压缩算法，http1.x的版本消息头带有大量的冗余消息
- http2.0 采用多路复用，即用一个tcp连接处理所有的请求，真正意义上做到了并发请求，流还支持优先级和流量控制（HTTP/1.x 虽然通过 pipeline也能并发请求，但是多个请求之间的响应会被阻塞的，所以 pipeline 至今也没有被普及应用，而 HTTP/2 做到了真正的并发请求。同时，流还支持优先级和流量控制。）
- http2.0支持server push，服务端可以主动把css，jsp文件主动推送到客户端，不需要客户端解析HTML，再发送请求，当客户端需要的时候，它已经在客户端了。


**缺点**

虽然 HTTP/2 解决了很多之前旧版本的问题，但是它还是存在一个巨大的问题， **主要是底层支撑的 TCP 协议造成的**
。HTTP/2的缺点主要有以下几点：

  * TCP 以及 TCP+TLS建立连接的延时

HTTP/2使用TCP协议来传输的，而如果使用HTTPS的话，还需要使用TLS协议进行安全传输，而使用TLS也需要一个握手过程，
**这样就需要有两个握手延迟过程** ：

①在建立TCP连接的时候，需要和服务器进行三次握手来确认连接成功，也就是说需要在消耗完1.5个RTT之后才能进行数据传输。

②进行TLS连接，TLS有两个版本——TLS1.2和TLS1.3，每个版本建立连接所花的时间不同，大致是需要1~2个RTT。

总之，在传输数据之前，我们需要花掉 3～4 个 RTT。

  * TCP的队头阻塞并没有彻底解决

上文我们提到在HTTP/2中，多个请求是跑在一个TCP管道中的。但当出现了丢包时，HTTP/2 的表现反倒不如 HTTP/1
了。因为TCP为了保证可靠传输，有个特别的“丢包重传”机制，丢失的包必须要等待重新传输确认，HTTP/2出现丢包时，整个 TCP
都要开始等待重传，那么就会阻塞该TCP连接中的所有请求（如下图）。而对于 HTTP/1.1 来说，可以开启多个 TCP
连接，出现这种情况反到只会影响其中一个连接，剩余的 TCP 连接还可以正常传输数据。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/20_04/20200714205644.png)

### Http 3.0

Google 在推SPDY的时候就已经意识到了这些问题，于是就另起炉灶搞了一个基于 UDP 协议的“QUIC”协议，让HTTP跑在QUIC上而不是TCP上。
而这个“HTTP over QUIC”就是HTTP协议的下一个大版本，HTTP/3。它在HTTP/2的基础上又实现了质的飞跃，真正“完美”地解决了“队头阻塞”问题。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/20_04/20200714210054.png)


QUIC 虽然基于 UDP，但是在原本的基础上新增了很多功能，接下来我们重点介绍几个QUIC新功能。不过HTTP/3目前还处于草案阶段，正式发布前可能会有变动，所以本文尽量不涉及那些不稳定的细节。


#### QUIC新功能

上面我们提到QUIC基于UDP，而UDP是“无连接”的，根本就不需要“握手”和“挥手”，所以就比TCP来得快。此外QUIC也实现了可靠传输，保证数据一定能够抵达目的地。它还引入了类似HTTP/2的“流”和“多路复用”，单个“流"是有序的，可能会因为丢包而阻塞，但其他“流”不会受到影响。具体来说QUIC协议有以下特点：

  * 实现了类似TCP的流量控制、传输可靠性的功能。

虽然UDP不提供可靠性的传输，但QUIC在UDP的基础之上增加了一层来保证数据可靠性传输。它提供了数据包重传、拥塞控制以及其他一些TCP中存在的特性。

  * 实现了快速握手功能。

由于QUIC是基于UDP的，所以QUIC可以实现使用0-RTT或者1-RTT来建立连接，这意味着QUIC可以用最快的速度来发送和接收数据，这样可以大大提升首次打开页面的速度。
**0RTT 建连可以说是 QUIC 相比 HTTP2 最大的性能优势** 。

  * 集成了TLS加密功能。

目前QUIC使用的是TLS1.3，相较于早期版本TLS1.3有更多的优点，其中最重要的一点是减少了握手所花费的RTT个数。

  * 多路复用，彻底解决TCP中队头阻塞的问题

和TCP不同，QUIC实现了在同一物理连接上可以有多个独立的逻辑数据流（如下图）。实现了数据流的单独传输，就解决了TCP中队头阻塞的问题。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/20_04/20200714210232.png)

关于 http 3.0 的，如果想了解更多，可以查看这一篇文章。[解密HTTP/2与HTTP/3 的新特性](https://juejin.im/post/5d9abde7e51d4578110dc77f)

### 总结

* HTTP/1.1有两个主要的缺点：安全不足和性能不高。
* HTTP/2完全兼容HTTP/1，是“更安全的HTTP、更快的HTTPS"，头部压缩、多路复用等技术可以充分利用带宽，降低延迟，从而大幅度提高上网体验；
* QUIC 基于 UDP 实现，是 HTTP/3 中的底层支撑协议，该协议基于 UDP，又取了 TCP 中的精华，实现了即快又可靠的协议


## http 状态码


Http 状态码 | 含义
---|---
200 | 请求成功
206 | 支持断点下载（range = byte = 0 -1024)
301 | 永远移动
302  | 临时移动
303	 | See Other	查看其它地址。与301类似。使用GET和POST请求查看
304 | 无更新
400 | Bad request,服务器无法识别
403 | 禁止访问
404 | not found
405	| Method Not Allowed	客户端请求中的方法被禁止
500	| Internal Server Error	服务器内部错误，无法完成请求

关于更详细的可以查看 

[http 状态码](https://www.runoob.com/http/http-status-codes.html)

## 参考链接

https://juejin.im/post/5d032b77e51d45777a126183

https://www.cnblogs.com/geass-jango/p/11458549.html

https://zhuanlan.zhihu.com/p/135947893

https://www.v2ex.com/t/373770

https://www.jianshu.com/p/f6b0cc69affc


## 题外话

下一篇预告，将会推出 面试官系列 - https 真的安全吗，可以抓包吗，如何防止抓包。

**有兴趣的话可以关注我的公众号 徐公码字（stormjun94）**

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/19_08/%E5%BE%90%E5%85%AC%E7%A0%81%E5%AD%97%202.jpeg)



 **目前从事于 Android 开发，除了分享 Android开发相关知识，还有职场心得，面试经验，学习心得，人生感悟等等。希望通过该公众号，让你看到程序猿不一样的一面，我们不只会敲代码，我们还会。。。。。。，期待你的参与**
 

  