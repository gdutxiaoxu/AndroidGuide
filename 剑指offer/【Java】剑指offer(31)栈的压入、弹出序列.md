# 【Java】 剑指offer(31) 栈的压入、弹出序列  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1、2、3、4、5是某栈的压栈序列，序列4、5、3、2、1是该压栈序列对应的一个弹出序列，但4、3、5、1、2就不可能是该压栈序列的弹出序列。

## 思路

建立一个栈，按照压栈序列依次进行入栈操作，按出栈序列的顺序依次弹出数字。在出栈时，若下一个要出栈的数字与栈顶数字相同则弹出。如果压栈序列中的所有数字都入栈后没有完全出栈成功则代表两个序列不匹配，返回false。

**测试算例** ****

1.功能测试（两个数组长度不同；两个数组对应；两个数组不对应）

2.特殊测试（数组为空；null；一个数字的数组）

## **Java代码**

    
    
    //题目：输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是
    //否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1、2、3、4、
    //5是某栈的压栈序列，序列4、5、3、2、1是该压栈序列对应的一个弹出序列，但
    //4、3、5、1、2就不可能是该压栈序列的弹出序列。
    
    public class StackPushPopOrder {
        public boolean isPopOrder(int [] pushA,int [] popA) {
        	if(pushA==null || popA==null)
        		return false;
        	Stack<Integer> stack = new Stack<Integer>();
        	//必须提前判断长度是否相等
        	if(popA.length!=pushA.length || pushA.length==0)
        		return false;
        	int popIndex=0;
        	for(int pushIndex=0; pushIndex<pushA.length; pushIndex++) {
        		stack.push(pushA[pushIndex]); 
        		while(!stack.empty() &&stack.peek()==popA[popIndex]) {
        			stack.pop();
        			popIndex++;
        		}
        	}
        	return stack.empty();
        }
    }   
    

## **收获**

通过举例子，整理清楚逻辑顺序：依次先入栈，再判断是否出栈；出栈序列能实现栈的清空说明两个序列匹配。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)