# 【Java】 剑指offer(23) 链表中环的入口结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

一个链表中包含环，如何找出环的入口结点？例如，在图3.8的链表中，环的入口结点是结点3。

## 思路

1.确定链表是否有环：通过两个不同速度的指针确定，当两个指针指向同一个结点时，该结点为环中的一个结点。

2.确定环中结点的数目n：指针走一圈，边走边计数

3.找到环的入口：从头结点开始，通过两个相差为n的指针来得到（即寻找链表中倒数第n个结点）

更简单的思路：[【LeetCode】142. Linked List Cycle
II](https://www.cnblogs.com/yongh/p/9981395.html "发布于2018-11-19 09:21")

**测试算例** ****

1.功能测试（链表包含与不包含环；链表有多个或一个结点）

2.特殊测试（头结点为null）

## **Java代码**

    
    
    package _23;
    /**
     * 
     * @Description 链表中环的入口结点 
     *
     * @author yongh
     * @date 2018年10月15日 下午2:35:14
     */
    
    //题目：一个链表中包含环，如何找出环的入口结点？例如，在图3.8的链表中，
    //环的入口结点是结点3。
    
    /*
     * 思路:1.确定链表是否有环：通过两个不同速度的指针确定
     * 	  	2.确定环中结点的数目n：指针走一圈，边走边计数
     * 		3.找到环的入口：从头结点开始，通过两个相差为n的指针来得到（即寻找链表中倒数第n个结点）
     */
    
    public class EntryNodeInListLoop {
    	 public class ListNode {
    		    int val;
    		    ListNode next = null;
    
    		    ListNode(int val) {
    		        this.val = val;
    		    }
    	 }
    	
    	/*
    	 * 确定链表是否有环，采用快慢指针确定
    	 * 返回值代表快慢指针相遇时的结点，返回null代表链表无环
    	 */
    	private ListNode meetingNode(ListNode head) {
    		if(head==null)
    			return null;
    		ListNode pSlow=head;
    		ListNode pFast=head;
    		while(pFast!=null) {
    			pSlow=pSlow.next;
    			pFast=pFast.next;
    			if(pFast!=null)
    				pFast=pFast.next;
    			if(pSlow!=null && pSlow==pFast)
    				return pSlow;
    		}
    		return null;		
    	}
    	
    	
    	/**
    	 * 计算环中入口结点
    	 */
    	public ListNode entryNodeOfLoop(ListNode head) {
    		ListNode meetingNode=meetingNode(head);
    		if(meetingNode==null)
    			return null;
    		
    		//计算环中结点的数目
    		int count=1;  //环中结点的数目
    		ListNode pNode1 = meetingNode.next;
    		while(pNode1!=meetingNode){
    			count++;
    			pNode1=pNode1.next;
    		}
    		
    		//先移动pNode1，次数为count
    		pNode1=head;
    		for(int i=1;i<=count;i++) {
    			pNode1=pNode1.next;
    		}
    		ListNode pNode2=head;
    		while(pNode1!=pNode2) {
    			pNode1=pNode1.next;
    			pNode2=pNode2.next;
    		}
    		return pNode1;		
    	}
    	
    }
    

## **收获**

1.通过两个不同速度的指针可以确定链表中是否有环

2.相差n步的两个指针可以找到倒数第n个结点链表中倒数第k个结点:https://www.cnblogs.com/yongh/p/9788286.html）

3.复杂问题分解成为几个简单问题（本题分为三步：找出环中任一结点；得到环的个数；找到入口结点）

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)