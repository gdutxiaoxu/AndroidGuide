# 【Java】 剑指offer(8) 用两个栈实现队列  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview **

## 题目

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数appendTail和deleteHead，分别完成在队列尾部插入结点和在队列头部删除结点的功能。

## 思路

这道题较简单，自己先试着模拟一下插入删除的过程（在草稿纸上动手画一下）：插入肯定是往一个栈stack1中一直插入；删除时，直接出栈无法实现队列的先进先出规则，这时需要将元素从stack1出栈，压到另一个栈stack2中，然后再从stack2中出栈就OK了。需要稍微注意的是：当stack2中还有元素，stack1中的元素不能压进来；当stack2中没元素时，stack1中的所有元素都必须压入stack2中。否则顺序就会被打乱。

**测试用例**

1.往空队列添加删除元素

2.往非空队列添加删除元素

3.删除至队列为空

## **完整Java代码**

（含测试代码）

    
    
    import java.util.Stack;
    
    /**
     * 
     * @Description 用两个栈实现队列 
     *
     * @author yongh
     * @date 2018年9月13日 下午2:17:22
     */
    
    // 题目：用两个栈实现一个队列。队列的声明如下，请实现它的两个函数appendTail
    // 和deleteHead，分别完成在队列尾部插入结点和在队列头部删除结点的功能。
    
    public class QueueWithTwoStacks {
    	
    	class Queue{
    	    Stack<Integer> stack1 = new Stack<Integer>();
    	    Stack<Integer> stack2 = new Stack<Integer>();
    	    
    	    /**
    	     * 插入结点
    	     */
    		public void push(int node) {
    			stack1.push(node);
    		}
    		
    		/**
    		 * 删除结点
    		 */
    		public int pop() {
    			if (stack2.empty()) {
    				if (stack1.empty())
    					throw new RuntimeException("队列为空！");
    				else {
    					while (!stack1.empty())
    						stack2.push(stack1.pop());
    				}
    			}
    			return stack2.pop();
    		}
    	}
    	
    	
    	//=======测试代码==========
    	
    	public void test1() {
    		Queue queue= new Queue();
     		queue.push(1);
     		queue.push(2);
    		System.out.println(queue.pop());
    		queue.push(3);
    		System.out.println(queue.pop());
    		System.out.println(queue.pop());
    	}
    	
    	/**
    	 * 往空队列删除元素
    	 */
    	public void test2() {
    		Queue queue= new Queue();
    		System.out.println(queue.pop());
    	}
    	
    	public static void main(String[] args) {
    		QueueWithTwoStacks demo = new QueueWithTwoStacks();
    		demo.test1();		
    		demo.test2();
    	}
    
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    1
    2
    3
    Exception in thread "main" java.lang.RuntimeException: 队列为空！

QueueWithTwoStacks

## **收获**

1.学会用画图将抽象问题形象化

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)