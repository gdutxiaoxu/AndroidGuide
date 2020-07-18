



## 前言

在讲解 http 与 https 之间的区别之前，我么先来看一下一个常见的面试问题。

**一次完整的 http 协议请求过程是怎样的**

![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMDUwMjAzLWEzZWRjNmYyOTljZjgzN2IuanBn)

该图片出自 [博客](https://blog.csdn.net/liudong8510/article/details/7908093)


## Http协议的主要特点

1. 支持客户／服务器模式
2. 简单快速：客户向服务端请求服务时，只需传送请求方式和路径。
3. 灵活：允许传输任意类型的数据对象。由Content-Type加以标记。
4. 无连接：每次响应一个请求，响应完成以后就断开连接。
5. 无状态：服务器不保存浏览器的任何信息。每次提交的请求之间没有关联。


[怎么理解HTTP协议是无状态的无连接的的协议？](https://www.jianshu.com/p/30744fbd1f01)

### 非持续性和持续性

HTTP1.0默认非持续性；HTTP1.1默认持续性

持续性：浏览器和服务器建立TCP连接后，可以请求多个对象

非持续性：浏览器和服务器建立TCP连接后，只能请求一个对象

### 非流水线和流水线

类似于组成里面的流水操作

* 流水线：不必等到收到服务器的回应就发送下一个报文。
* 非流水线：发出一个报文，等到响应，再发下一个报文。类似TCP。


### http 各个版本之间的区别

1.0 与 1.1

- http1.0一次只能处理一个请求，不能同时收发数据
- http1.1可以处理多个请求，能同时收发数据
- http1.1增加可更多字段，如cache-control,keep-alive.

2.0

- http 2.0采用二进制的格式传送数据，不再使用文本格式传送数据
- http2.0对消息头采用hpack压缩算法，http1.x的版本消息头带有大量的冗余消息
- http2.0 采用多路复用，即用一个tcp连接处理所有的请求，真正意义上做到了并发请求，流还支持优先级和流量控制（HTTP/1.x 虽然通过 pipeline也能并发请求，但是多个请求之间的响应会被阻塞的，所以 pipeline 至今也没有被普及应用，而 HTTP/2 做到了真正的并发请求。同时，流还支持优先级和流量控制。）
- http2.0支持server push，服务端可以主动把css，jsp文件主动推送到客户端，不需要客户端解析HTML，再发送请求，当客户端需要的时候，它已经在客户端了。


### POST和GET的区别

| Post一般用于更新或者添加资源信息       | Get一般用于查询操作，而且应该是安全和幂等的           |
| ------------- |:-------------:|
| Post更加安全      | Get会把请求的信息放到URL的后面 |
| Post传输量一般无大小限制     | Get不能大于2KB      |
| Post执行效率低 | Get执行效率略高      |


### 为什么POST效率低，Get效率高

* Get将参数拼成URL,放到header消息头里传递
* Post直接以键值对的形式放到消息体中传递。
* 但两者的效率差距很小很小


---

## Https

HTTPS相当于HTTP的安全版本了，是在http的基础之上加上ssl（Secure Socket Layer）

* 端口号是443
* 是由SSL+Http协议构建的可进行加密传输、身份认证的网络协议。

https在客户端（浏览器）与服务端（网站）传输加密的数据大概经历一下流程
1. 客户端将自己的has算法和加密算法发给服务器
2. 服务器接收到客户端发来的加密算法和has算法，取出自己的加密算法与has算法，并将自己的身份信息以证书的形式发送给客户端，该证书信息包括公钥，网站地址，预计颁发机构等
3. 客户端收到服务器发来的证书（即公钥），开始验证证书的合法性，如果证书信任，则生成一串随机的字符串数字作为私钥，并将私钥（密文）用证书（服务器的公钥）进行加密，发送给服务器
4. 服务器收到客户端发来的数据之后，通过服务器自己的私钥进行解密客户端发来的数据（客户端的私钥），（这样双方都拥有私钥）再进行hash检验，如果结果一致，则将客户端发来的字符串（第3个步骤发送过来的字符串）通过加密发送给客户端
5. 客户端解密，如果一致的话，就使用之前客户端随机生成的字符串进行对称加密算法进行加密


![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMDUwMjAzLTcxZGRmM2M2MjZjYjQyNGUucG5n)


---



## 推荐阅读

[聊一聊 Android 中巧妙的位操作](https://blog.csdn.net/gdutxiaoxu/article/details/84898590)

[二分查找的相关算法题](https://blog.csdn.net/gdutxiaoxu/article/details/51292440)

[快速排序的相关算法题（java）](https://blog.csdn.net/gdutxiaoxu/article/details/51299994)

[Android 面试必备 - 计算机网络基本知识（TCP，UDP，Http，https）](https://blog.csdn.net/gdutxiaoxu/article/details/97618598)

[360面试总结（Android）](https://blog.csdn.net/gdutxiaoxu/article/details/52371834)

![Android 技术人(stormjun94)](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8yMDUwMjAzLWMyNGQ5Y2RkNzBiMDEzMDcuanBn)

**扫一扫，欢迎关注我的公众号 stormjun94。如果你有好的文章，也欢迎你的投稿。**










