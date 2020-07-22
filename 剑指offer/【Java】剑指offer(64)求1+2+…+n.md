# 【Java】 剑指offer(64) 求1+2+…+n  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

求1+2+…+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

## 思路

不能使用乘除法，不能使用循环语句、判断语句。可以考虑的有 单目运算符：++和--,双目运算符：+,-，移位运算符
<<和>>，关系运算符>,<等，逻辑运算符&&，||,&,|,^，赋值=

最有可能使用到的就是逻辑运算符了。如果记得它们有短路特性的话，就可以当作if来使用了。

例如：对于A && B，如果A为假，那么就不执行B了；而如果A为真，就会执行B。

对于A || B，如果A为真，那么就会不执行B了；而如果A为假，就会执行B。

因此我们使用递归来代替循环，用逻辑运算符&&或者||来代替判断语句。

代码实现功能为：当n大于1时，和为f(n)=f(n-1)+n，n=1时，f(n)=1

## **Java代码**

    
    
    //题目：求1+2+…+n，要求不能使用乘除法、for、while、if、else、switch、case
    //等关键字及条件判断语句（A?B:C）。
    
    public class Accumulate {
    	public int getSum(int n) {
    		int sum=n;
    		boolean flag = (n>1) && ((sum+=getSum(n-1))>0);	
    		//上面这句话相当于：
    		//if(n>1)
    		//	 sum+=getSum(n-1);
    		
    		//也可以使用||来实现
    		//boolean flag = (n==1) || ((sum+=getSum(n-1))>0);	
    		return sum;
    	}
    }
    

## **收获**

1.学会利用 &&和||的短路特性来代替判断语句；

2.使用短路特性时，记得后面的判断语句要写完整

即：不能只写了`(sum+=getSum(n-``1``))，要完整写出`(sum+=getSum(n-``1``))``>``0``

还有就是前面要赋值给flag才算完整的语句。

3.利用递归来代替循环。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)