# 【Java】 剑指offer(30) 包含min函数的栈  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的min函数。在该栈中，调用min、push及pop的时间复杂度都是O(1)。

## 思路

最初想法是定义一个成员变量min来存放最小元素，但是当最小元素弹出后，min就需要相应改变，所以必须把每次的最小值都存储下来。考虑采用一个辅助栈来存放最小值：

栈 3，4，2，5，1

辅助栈 3， 3，2，2，1

（压入时，把每次的最小元素（之前最小元素与新入栈元素的较小值）保存起来放到辅助栈中）

**测试算例** ****

1.新压入数字更大

2.新压入数字最小

3.弹出数字最小

4.弹出数字不是最小

## **Java代码**

    
    
    //题目：定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的min
    //函数。在该栈中，调用min、push及pop的时间复杂度都是O(1)。
    
    public class StackWithMin {
    	
    	Stack<Integer> stack_data=new Stack<Integer>();
    	Stack<Integer> stack_min=new Stack<Integer>();
    
        public void push(int node) {
            stack_data.push(node);
            if(stack_min.empty() || stack_min.peek()>node) {
            	stack_min.push(node);
            }else {
            	stack_min.push(stack_min.peek());
            }        
        }
        
        public void pop() {
        	if(!stack_data.empty()) {
                stack_data.pop();
                stack_min.pop();
        	}
        }    
     
        public int min() {
            return stack_min.peek();
        }
    }
    

## **收获**

要学会这种情况下辅助栈的用法。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)