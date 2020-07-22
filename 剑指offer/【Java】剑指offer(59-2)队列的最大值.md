# 【Java】 剑指offer(59-2) 队列的最大值  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请定义一个队列并实现函数max得到队列里的最大值，要求函数max、push_back和pop_front的时间复杂度都是O(1)。

## 思路

滑动窗口的最大值:https://www.cnblogs.com/yongh/p/9964581.html一题相似，利用一个双端队列来存储当前队列里的最大值以及之后可能的最大值。

在定义题目要求功能的队列时，除了定义一个队列data存储数值，还需额外用一个队列maxmium存储可能的最大值；此外，还要定义一个数据结构，用于存放数据以及当前的index值，用于删除操作时确定是否删除maxmium中最大值。

具体实现见代码，代码进行了一些测试，应该没有什么问题。

**测试算例** ****

尾部插入不同大小数字，删除头部数字。插入删除同时获取最大值。

## **Java代码**

    
    
    import java.util.ArrayDeque;
    
    //题目：请定义一个队列并实现函数max得到队列里的最大值，要求函数max、
    //push_back和pop_front的时间复杂度都是O(1)。
    
    public class QueueWithMax {
    	private ArrayDeque<InternalData>  data = new ArrayDeque<InternalData>();
    	private ArrayDeque<InternalData> maximum = new ArrayDeque<InternalData>();
    	private class InternalData{
    		int number;
    		int index;
    		public InternalData(int number,int index) {
    			this.number=number;
    			this.index=index;
    		}
    	}
    	private int curIndex;
    	
    	public void push_back(int number) {
    		InternalData curData = new InternalData(number,curIndex);
    		data.addLast(curData);
    		
    		while(!maximum.isEmpty() && maximum.getLast().number<number)
    			maximum.removeLast();
    		maximum.addLast(curData);
    		
    		curIndex++;  //别漏了这句
    	}
    	
    	public void pop_front() {
    		if(data.isEmpty()) {
    			System.out.println("队列为空，无法删除！");
    			return;
    		}
    		InternalData curData = data.removeFirst();
    		if(curData.index==maximum.getFirst().index)
    			maximum.removeFirst();
    	}
    	
    	public int max() {
    		if(maximum==null){
    			System.out.println("队列为空，无法删除！");
    			return 0;
    		}
    		return maximum.getFirst().number;
    	}
    	
    	public static void main(String[] args) {
    		QueueWithMax testQueue = new QueueWithMax();
    	    // {2}
    	    testQueue.push_back(2);
    	    System.out.println(testQueue.max()==2);
    	    // {2, 3}
    	    testQueue.push_back(3);
    	    System.out.println(testQueue.max()==3);
    	    // {2, 3, 4}
    	    testQueue.push_back(4);
    	    System.out.println(testQueue.max()==4);
    	    // {2, 3, 4, 2}
    	    testQueue.push_back(2);
    	    System.out.println(testQueue.max()==4);
    	    // {3, 4, 2}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==4);
    	    // {4, 2}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==4);
    	    // {2}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==2);
    	    // {2, 6}
    	    testQueue.push_back(6);
    	    System.out.println(testQueue.max()==6);
    	    // {2, 6, 2}
    	    testQueue.push_back(2);
    	    System.out.println(testQueue.max()==6);
    	    // {2, 6, 2, 5}
    	    testQueue.push_back(5);
    	    System.out.println(testQueue.max()==6);
    	    // {6, 2, 5}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==6);
    	    // {2, 5}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==5);
    	    // {5}
    	    testQueue.pop_front();
    	    System.out.println(testQueue.max()==5);
    	    // {5, 1}
    	    testQueue.push_back(1);
    	    System.out.println(testQueue.max()==5);	    
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
     true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true

QueueWithMax

## **收获**

1.在定义 private ArrayDeque<InternalData> data时，别忘记了new
ArrayDeque<InternalData>();否则在插入数据时，会抛出NPE异常。

2.进行删除操作时，注意是否队列是否为空。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)