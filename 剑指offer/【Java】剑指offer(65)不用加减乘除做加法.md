# 【Java】 剑指offer(65) 不用加减乘除做加法  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

写一个函数，求两个整数之和，要求在函数体内不得使用＋、－、×、÷四则运算符号。

## 思路

对数字做运算，除了四则运算外，只剩下位运算了。根据一般情况下的加法步骤，设计如下：

1）不考虑进位对每一位相加：1加0，0加1都等于1，而0加0，1加1等于0，所以使用异或^操作；

2）计算进位：只有1加1产生进位，所以采用位与 &操作，再左移1位；

3）将和与进位相加，即重复前两步操作。结束判断为进位为0。

**测试代码**

1.正负零

## **Java代码**

    
    
    //题目：写一个函数，求两个整数之和，要求在函数体内不得使用＋、－、×、÷
    //四则运算符号。
    
    public class AddTwoNumbers {
        public int add(int num1,int num2) {
            while(num2!=0){
                int sum=num1^num2;  //没进位的和
                int carry=(num1&num2)<<1;  //进位
                num1=sum;
                num2=carry;
            }
            return num1;
        }
    }
    

## **收获**

1.熟悉位操作的特性二进制位运算的几个用法:https://www.cnblogs.com/yongh/p/9971520.html

2.记住如何用位操作来进行数字的加减。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)