# 【Java】 剑指offer(24) 反转链表  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

定义一个函数，输入一个链表的头结点，反转该链表并输出反转后链表的头结点。

## 思路

方法一：使用三个指针（pre,p,next）进行实现。令p指向pre，next则是用于防止链表断裂（很简单，详见代码）。

方法二（递归）：找到最后一个结点作为返回值，递归函数中，找到最后的头结点后，开始进行每个结点next值的转换。

**测试算例** ****

1.功能测试（链表有多个或一个结点）

2.特殊测试（头结点为null）

## **Java代码**

新：

    
    
        //iteratively
        public ListNode reverseList(ListNode head) {
            ListNode pre = null;
            ListNode cur = head;
            while(cur!=null){
                ListNode next = cur.next;
                cur.next = pre;
                pre = cur;
                cur = next;
            }
            return pre;
        }
        //recursively
        public ListNode reverseList1(ListNode head) {
            if(head == null || head.next==null)
                return head;
            ListNode newHead = reverseList(head.next);
            head.next.next = head;
            head.next = null;
            return newHead;
        }
    

旧：

    
    
    package _24;
    /**
     * 
     * @Description 面试题24：反转链表
     *
     * @author yongh
     * @date 2018年10月15日 下午3:24:51
     */
    
    //题目：定义一个函数，输入一个链表的头结点，反转该链表并输出反转后链表的
    //头结点。
    
    public class ReverseList {
    	public class ListNode {
    		int val;
    		ListNode next=null;
    		ListNode(int val){
    			this.val=val;			
    		}
    	}
    	
    	/*
    	 * 三个指针实现
    	 */
    	public ListNode reverseList(ListNode head) {
    		if(head==null)
    			return null;
    		ListNode pNode=head;
    		ListNode preNode=null;
    		ListNode nextNode=pNode.next;
    		while(nextNode!=null) {
    			pNode.next=preNode;
    			preNode=pNode;
    			pNode=nextNode;
    			nextNode=pNode.next;
    		}
    		pNode.next=preNode;
    		return pNode;
    	}
    	
    	/*
    	 * 递归实现
    	 */
    	public ListNode reverseList2(ListNode head) {
    		if(head==null || head.next==null)
    			return head;
    		ListNode rvsHead=reverseList(head.next);
    		//找到了最后的头结点后，开始转换每个结点的指向
    		head.next.next=head;
    		head.next=null;		
    		return rvsHead;
    	}
    	
    }
    

## **收获**

1.与链表相关的题目总是涉及大量指针操作，以后遇到链表相关的题目时，多考虑指针的使用。

2.递归实现时，第50行：`head.next=``null``;  别忘记了。`

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)