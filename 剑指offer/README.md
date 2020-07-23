> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview


## 前言

现如今，如果你想进入大厂，腾讯，阿里，头条，拼多多等，不管是社招还是校招，肯定都会面试到算法的。

相信很多人有这样的想法，面试的时候早火箭，工作的时候拧螺丝。确实，这种情况非常常见，我也认同。但没办法，谁叫我们想进入大厂呢，主动权掌握在人家手里。

不过，这种情况也可以理解。怎么在几轮面试中确定面试者的水平呢？
肯定是考察算法，基础这些，原理这些。

虽然这些代表不了全部，但起码能在一定程度上代表了面试者的水平能力。要知道，编程语言其实都是想通的，数据结果和算法能力才是核心。掌握了原理，编程思维，切换到另外一门语言其实是很快的。这也就是面试官喜欢考察算法和原理的原因。

至于要怎么学习算法，我简单归纳一下
1. 第一，要了解基本的数据结果，数组，聊表，Map，Set，二叉树等，了解他们的优缺点，时间复杂度，空间复杂度等
2. 第二，要掌握一些常见的算法，递归，迭代，八大排序，二分查找，贪心算法等
3. 第三，掌握一种算法，不仅要知道 what，还要知道 why（分析各种算法的优缺点），比如 topK问题，有常见的几种解决方案，排序，快排思想，海量数据堆排序
4. 刚开始学的时候，可能会比较吃力，可以先刷题，慢慢找感觉，从易到难。比如，第一天，你刷这道算法题的时候看不懂，先不用着急，很多人都是这样过来的，先搜一下答案，看一下别人是怎么解决的。看懂了之后，**自己用代码写一遍，跑一遍**。这很重要，很多时候，你以为你自己懂了，但当你在写的时候是写不出来的，在你动手写代码时，会不断加深你的印象。第二天，自己再写一遍，加深印象
5. 学好算法不是一日之功，需要长期的积累。建议的做法是每天做一两道题，题目不在多，贵在于理解。坚持一两个月，你会发现你的感觉逐渐好起来了。


不知不觉说了好多，改天有空的时候再写一篇文章，如何学好算法，以及整理算法常见的题目。有兴趣的可以关注我的**微信公众号徐公码字（stormjun94）**

下面开始进入正题，本期为大家整理了剑指offer的全部算法题目，全部用 java 语言实现。如果你觉得对你有帮助的话，欢迎大家到 github 帮我 star，谢谢大家，你们的支持就是我写作的最大动力。

https://github.com/gdutxiaoxu/Android_interview

## 目录


- [Android基础](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android_interview/Android基础)
    - [Android面试必备-JVM及类加载机制.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-JVM及类加载机制.md)
    - [Android面试必备-http与https协议.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-http与https协议.md)
    - [Android面试必备-系统、App、Activity启动过程.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-系统、App、Activity启动过程.md)
    - [Android面试必备-线程.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-线程.md)
    - [Android面试必备-计算机网络基本知识.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-计算机网络基本知识.md)
    - [Android面试必备-计算机网络基本知识（TCP，UDP，Http，https）.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/Android面试必备-计算机网络基本知识（TCP，UDP，Http，https）.md)
    - [面试官系列-你真的了解http吗.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/面试官系列-你真的了解http吗.md)
    - [面试官问，https真的安全吗，可以抓包吗，如何防止抓包吗.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android基础/面试官问，https真的安全吗，可以抓包吗，如何防止抓包吗.md)
- [README.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android_interview/README.md)
- [剑指offer](https://github.com/gdutxiaoxu/Android_interview/tree/master/Android_interview/剑指offer)
    - [【Java】剑指offer(1)找出数组中重复的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(1)找出数组中重复的数字.md)
    - [【Java】剑指offer(2)不修改数组找出重复的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(2)不修改数组找出重复的数字.md)
    - [【Java】剑指offer(3)二维数组中的查找.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(3)二维数组中的查找.md)
    - [【Java】剑指offer(4)替换空格.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(4)替换空格.md)
    - [【Java】剑指offer(5)从尾到头打印链表.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(5)从尾到头打印链表.md)
    - [【Java】剑指offer(6)重建二叉树.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(6)重建二叉树.md)
    - [【Java】剑指offer(7)二叉树的下一个结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(7)二叉树的下一个结点.md)
    - [【Java】剑指offer(8)用两个栈实现队列.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(8)用两个栈实现队列.md)
    - [【Java】剑指offer(9)斐波那契数列及青蛙跳台阶问题.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(9)斐波那契数列及青蛙跳台阶问题.md)
    - [【Java】剑指offer(10)旋转数组的最小数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(10)旋转数组的最小数字.md)
    - [【Java】剑指offer(11)矩阵中的路径.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(11)矩阵中的路径.md)
    - [【Java】剑指offer(12)机器人的运动范围.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(12)机器人的运动范围.md)
    - [【Java】剑指offer(13)剪绳子.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(13)剪绳子.md)
    - [【Java】剑指offer(14)二进制中1的个数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(14)二进制中1的个数.md)
    - [【Java】剑指offer(15)数值的整数次方.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(15)数值的整数次方.md)
    - [【Java】剑指offer(16)打印1到最大的n位数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(16)打印1到最大的n位数.md)
    - [【Java】剑指offer(17)在O(1)时间删除链表结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(17)在O(1)时间删除链表结点.md)
    - [【Java】剑指offer(18)删除链表中重复的结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(18)删除链表中重复的结点.md)
    - [【Java】剑指offer(19)正则表达式匹配.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(19)正则表达式匹配.md)
    - [【Java】剑指offer(20)表示数值的字符串.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(20)表示数值的字符串.md)
    - [【Java】剑指offer(21)调整数组顺序使奇数位于偶数前面.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(21)调整数组顺序使奇数位于偶数前面.md)
    - [【Java】剑指offer(22)链表中倒数第k个结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(22)链表中倒数第k个结点.md)
    - [【Java】剑指offer(23)链表中环的入口结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(23)链表中环的入口结点.md)
    - [【Java】剑指offer(24)反转链表.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(24)反转链表.md)
    - [【Java】剑指offer(25)合并两个排序的链表.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(25)合并两个排序的链表.md)
    - [【Java】剑指offer(26)树的子结构.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(26)树的子结构.md)
    - [【Java】剑指offer(27)二叉树的镜像.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(27)二叉树的镜像.md)
    - [【Java】剑指offer(28)对称的二叉树.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(28)对称的二叉树.md)
    - [【Java】剑指offer(29)顺时针打印矩阵.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(29)顺时针打印矩阵.md)
    - [【Java】剑指offer(30)包含min函数的栈.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(30)包含min函数的栈.md)
    - [【Java】剑指offer(31)栈的压入、弹出序列.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(31)栈的压入、弹出序列.md)
    - [【Java】剑指offer(32)从上往下打印二叉树.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(32)从上往下打印二叉树.md)
    - [【Java】剑指offer(33)二叉搜索树的后序遍历序列.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(33)二叉搜索树的后序遍历序列.md)
    - [【Java】剑指offer(34)二叉树中和为某一值的路径.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(34)二叉树中和为某一值的路径.md)
    - [【Java】剑指offer(35)复杂链表的复制.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(35)复杂链表的复制.md)
    - [【Java】剑指offer(36)二叉搜索树与双向链表.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(36)二叉搜索树与双向链表.md)
    - [【Java】剑指offer(37)序列化二叉树.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(37)序列化二叉树.md)
    - [【Java】剑指offer(38)字符串的排列.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(38)字符串的排列.md)
    - [【Java】剑指offer(39)数组中出现次数超过一半的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(39)数组中出现次数超过一半的数字.md)
    - [【Java】剑指offer(40)最小的k个数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(40)最小的k个数.md)
    - [【Java】剑指offer(41)数据流中的中位数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(41)数据流中的中位数.md)
    - [【Java】剑指offer(42)连续子数组的最大和.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(42)连续子数组的最大和.md)
    - [【Java】剑指offer(43)从1到n整数中1出现的次数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(43)从1到n整数中1出现的次数.md)
    - [【Java】剑指offer(44)数字序列中某一位的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(44)数字序列中某一位的数字.md)
    - [【Java】剑指offer(45)把数组排成最小的数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(45)把数组排成最小的数.md)
    - [【Java】剑指offer(46)把数字翻译成字符串.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(46)把数字翻译成字符串.md)
    - [【Java】剑指offer(47)礼物的最大价值.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(47)礼物的最大价值.md)
    - [【Java】剑指offer(48)最长不含重复字符的子字符串.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(48)最长不含重复字符的子字符串.md)
    - [【Java】剑指offer(50-1)字符串中第一个只出现一次的字符.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(50-1)字符串中第一个只出现一次的字符.md)
    - [【Java】剑指offer(50-2)字符流中第一个只出现一次的字符.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(50-2)字符流中第一个只出现一次的字符.md)
    - [【Java】剑指offer(51)数组中的逆序对.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(51)数组中的逆序对.md)
    - [【Java】剑指offer(52)两个链表的第一个公共结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(52)两个链表的第一个公共结点.md)
    - [【Java】剑指offer(53-1)数字在排序数组中出现的次数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(53-1)数字在排序数组中出现的次数.md)
    - [【Java】剑指offer(53-2)0到n-1中缺失的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(53-2)0到n-1中缺失的数字.md)
    - [【Java】剑指offer(53-3)数组中数值和下标相等的元素.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(53-3)数组中数值和下标相等的元素.md)
    - [【Java】剑指offer(54)二叉搜索树的第k个结点.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(54)二叉搜索树的第k个结点.md)
    - [【Java】剑指offer(55-1)二叉树的深度.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(55-1)二叉树的深度.md)
    - [【Java】剑指offer(55-2)平衡二叉树.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(55-2)平衡二叉树.md)
    - [【Java】剑指offer(56-1)数组中只出现一次的两个数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(56-1)数组中只出现一次的两个数字.md)
    - [【Java】剑指offer(56-2)数组中唯一只出现一次的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(56-2)数组中唯一只出现一次的数字.md)
    - [【Java】剑指offer(57-1)和为s的两个数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(57-1)和为s的两个数字.md)
    - [【Java】剑指offer(57-2)为s的连续正数序列.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(57-2)为s的连续正数序列.md)
    - [【Java】剑指offer(58-1)翻转单词顺序.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(58-1)翻转单词顺序.md)
    - [【Java】剑指offer(58-2)左旋转字符串.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(58-2)左旋转字符串.md)
    - [【Java】剑指offer(59-1)滑动窗口的最大值.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(59-1)滑动窗口的最大值.md)
    - [【Java】剑指offer(59-2)队列的最大值.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(59-2)队列的最大值.md)
    - [【Java】剑指offer(60)n个骰子的点数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(60)n个骰子的点数.md)
    - [【Java】剑指offer(61)扑克牌的顺子.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(61)扑克牌的顺子.md)
    - [【Java】剑指offer(62)圆圈中最后剩下的数字.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(62)圆圈中最后剩下的数字.md)
    - [【Java】剑指offer(63)股票的最大利润.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(63)股票的最大利润.md)
    - [【Java】剑指offer(64)求1+2+…+n.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(64)求1+2+…+n.md)
    - [【Java】剑指offer(65)不用加减乘除做加法.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(65)不用加减乘除做加法.md)
    - [【Java】剑指offer(66)构建乘积数组.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(66)构建乘积数组.md)
    - [【Java】剑指offer(67)把字符串转换成整数.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(67)把字符串转换成整数.md)
    - [【Java】剑指offer(68)树中两个结点的最低公共祖先.md](https://github.com/gdutxiaoxu/Android_interview/tree/master/剑指offer/【Java】剑指offer(68)树中两个结点的最低公共祖先.md)





---

## 题外话


最后再啰嗦一句，大家有兴趣的可以关注我的微信公众号，这个仓库会不断更新，主要是更新面试相关的东西。包括面试经验，算法等等。

https://github.com/gdutxiaoxu/Android_interview/edit/master/README.md

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)