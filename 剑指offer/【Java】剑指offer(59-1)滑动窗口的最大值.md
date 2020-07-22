# 【Java】 剑指offer(59-1) 滑动窗口的最大值  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

给定一个数组和滑动窗口的大小，请找出所有滑动窗口里的最大值。例如，如果输入数组{2, 3, 4, 2, 6, 2, 5,
1}及滑动窗口的大小3，那么一共存在6个滑动窗口，它们的最大值分别为{4, 4, 6, 6, 6, 5}

## 思路

蛮力直接在每个滑动窗口依次比较找出最大值，时间复杂度太高。

我们考虑把每个可能成为最大值的数字记录下来，就可以快速的得到最大值。

**思路：** 建立一个两端开口的队列，放置 **所有可能是最大值的数字** （存放的其实是对应的下标），且最大值位于队列开头。从头开始扫描数组，

如果遇到的数字比队列中所有的数字都大，那么它就是最大值，其它数字不可能是最大值了，将队列中的所有数字清空，放入该数字，该数字位于队列头部；

如果遇到的数字比队列中的所有数字都小，那么它还有可能成为之后滑动窗口的最大值，放入队列的末尾；

如果遇到的数字比队列中最大值小，最小值大，那么将比它小数字不可能成为最大值了，删除较小的数字，放入该数字。

由于滑动窗口有大小，因此，队列头部的数字如果其下标离滑动窗口末尾的距离大于窗口大小，那么也删除队列头部的数字。

**注** ：队列中存放的是下标，以上讲的 队列头部的数字 均指 队列头部的下标所指向的数字。写代码时不要弄混了。

**测试算例** ****

1.功能测试（数组数字递增、递减、无序）

2.边界值测试（滑动窗口大小位0、1、大于或者等于数组长度）

3.特殊输入测试（null）

## **Java代码**

    
    
    //题目：给定一个数组和滑动窗口的大小，请找出所有滑动窗口里的最大值。例如，
    //如果输入数组{2, 3, 4, 2, 6, 2, 5, 1}及滑动窗口的大小3，那么一共存在6个
    //滑动窗口，它们的最大值分别为{4, 4, 6, 6, 6, 5}，
    
    public class MaxInSlidingWindow {
        public ArrayList<Integer> maxInWindows(int [] num, int size){
            ArrayList<Integer> max = new ArrayList<Integer>();
            if(num==null || num.length<=0 || size<=0 || size>num.length)
                return max;
            ArrayDeque<Integer> indexDeque = new ArrayDeque<Integer>();
            
            for(int i=0;i<size-1;i++){
                while(!indexDeque.isEmpty() && num[i]> num[indexDeque.getLast()])
                    indexDeque.removeLast();
                indexDeque.addLast(i);
            }
            
            for(int i=size-1;i<num.length;i++){
                while(!indexDeque.isEmpty() && num[i]> num[indexDeque.getLast()])
                    indexDeque.removeLast();
                if(!indexDeque.isEmpty() && (i-indexDeque.getFirst())>=size)
                    indexDeque.removeFirst();
                indexDeque.addLast(i);
                max.add(num[indexDeque.getFirst()]);
            }
            
            return max;
        }
    }
    

## **收获**

1.自己最初想到的是只存放最大的数，没有想到可以存放所有可能是最大的数，要记住。

2.ArrayDeque——双端队列，要记住。下面是一些常用的方法：

![](https://img2018.cnblogs.com/blog/1407330/201811/1407330-20181115165621790-67013616.png)

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)