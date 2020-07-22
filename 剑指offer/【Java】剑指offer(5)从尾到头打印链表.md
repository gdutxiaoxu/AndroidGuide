# 【Java】 剑指offer(5) 从尾到头打印链表  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

## 题目

输入一个链表的头结点，从尾到头反过来打印出每个结点的值。结点定义如下：

    
    
     public class ListNode {
        int val;
        ListNode next = null;
    
        ListNode(int val) {
            this.val = val;
        }
    }

## 思路

结点遍历顺序只能从头到尾，但是输出的顺序却为从尾到头，是典型的“后进先出”问题，这就要联想到使用栈，从而也可以联想到使用递归。

**测试用例**

1.功能测试（单个结点链表，多个结点链表）

2.特殊输入测试（链表为空）

## **完整Java代码**

    
    
    import java.util.Stack;
    
    /**
     * 
     * @Description 从尾到头打印链表
     *
     * @author yongh
     * @date 2018年9月10日 下午7:07:23
     */
    
    //题目：输入一个链表的头结点，从尾到头反过来打印出每个结点的值。
    
    public class PrintListInReversedOrder {
    	class ListNode{
    		int key;
    		ListNode next;
    		public ListNode(int key) {
    			this.key=key;
    			this.next=null;
    		}
    	}
    	
    	// 采用栈
    	public void printListReversingly_Iteratively(ListNode node) {
    		Stack<ListNode> stack = new Stack<ListNode>();
    		while (node!= null) {
    			stack.push(node);
    			node=node.next;
    		}
    		while(!stack.empty()) {
    			System.out.println(stack.pop().key);
    		}
    	}
    	
    	//采用递归
    	public void printListReversingly_Recursively(ListNode node) {
    		if(node!=null) {
    			printListReversingly_Recursively(node.next);
    			System.out.println(node.key);
    		}else
    			return;
    		
    	}
    	
    	
    	// ==================================测试代码==================================
    	/**
    	 * 链表为空
    	 */
    	public void test1() {
    		ListNode aListNode = null;
    		System.out.println("采用栈：");
    		printListReversingly_Iteratively(aListNode);
    		System.out.println("采用递归：");
    		printListReversingly_Recursively(aListNode);
    	}
    	
    	/**
    	 * 多个结点链表
    	 */
    	public void test2() {
    		ListNode ListNode1 = new ListNode(1);
    		ListNode ListNode2 = new ListNode(2);
    		ListNode ListNode3 = new ListNode(3);
    		ListNode ListNode4 = new ListNode(4);
    		ListNode ListNode5 = new ListNode(5);
    		ListNode1.next=ListNode2;
    		ListNode2.next=ListNode3;
    		ListNode3.next=ListNode4;
    		ListNode4.next=ListNode5;
    		System.out.println("采用栈：");
    		printListReversingly_Iteratively(ListNode1);
    		System.out.println("采用递归：");
    		printListReversingly_Recursively(ListNode1);
    	}
    	
    	/**
    	 * 单个结点链表
    	 */
    	public void test3() {
    		ListNode ListNode1 = new ListNode(1);
    		System.out.println("采用栈：");
    		printListReversingly_Iteratively(ListNode1);
    		System.out.println("采用递归：");
    		printListReversingly_Recursively(ListNode1);
    	}
    	
    	public static void main(String[] args) {
    		PrintListInReversedOrder demo = new PrintListInReversedOrder();
    		System.out.println("test1:");
    		demo.test1();
    		System.out.println("test2:");
    		demo.test2();
    		System.out.println("test3:");
    		demo.test3();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
     test1:
    采用栈：
    采用递归：
    test2:
    采用栈：
    5
    4
    3
    2
    1
    采用递归：
    5
    4
    3
    2
    1
    test3:
    采用栈：
    1
    采用递归：
    1

PrintListInReversedOrder

递归部分代码也可以像下面这样写，注意体会不同的递归写法：

    
    
    	// 采用递归
    	public void printListReversingly_Recursively(ListNode node) {
    		// if(node!=null) {
    		// printListReversingly_Recursively(node.next);
    		// System.out.println(node.key);
    		// }else
    		// return;
    		if (node != null) {
    			if (node.next != null) {
    				printListReversingly_Recursively(node.next);
    			}
    			System.out.println(node.key);
    		}
    	}
    

====================================================================

在牛客网中提交的代码如下（参考自grass_stars:https://www.nowcoder.com/profile/146839 的代码）：

    
    
    public class Solution {
    	ArrayList<Integer> arrayList = new ArrayList<Integer>();
    	public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
    		if (listNode != null) {
    			this.printListFromTailToHead(listNode.next);
    			arrayList.add(listNode.val);
    		}
    		return arrayList;
    	}
    }
    

上面代码采用的递归，非常简洁，很值得学习。

## **收获**

1.对于“后进先出”问题，要快速想到”栈“，也同时想到递归。

2.采用递归时，返回的函数值不一定要有赋值操作，只要实现了遍历的作用就可以了，上面牛客网的代码可以多多学习。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)