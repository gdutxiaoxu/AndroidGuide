# 【Java】 剑指offer(25) 合并两个排序的链表  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入两个递增排序的链表，合并这两个链表并使新链表中的结点仍然是按照递增排序的。

## 思路

**递归实现**
：合并过程中，每次都是从两个链表中找出较小的一个来链接，因此可以采用递归来实现：当任意一个链表为null时，直接链接另一个链表即可；其余情况只需要在两个链表中找出较小的一个结点进行链接，该结点的next值继续通过递归函数来链接。

**非递归实现：** 非递归实现比较容易想到，直接进行分情况讨论即可，要稍微注意下后面代码中头结点的赋值过程。

**测试算例** ****

1.功能测试（两个链表有多个或一个结点；结点值相同、不同）

2.特殊测试（任意一个或者两个链表的头结点为null）

## **Java代码**

    
    
    //题目：输入两个递增排序的链表，合并这两个链表并使新链表中的结点仍然是按
    //照递增排序的。
    
    public class MergeSortedLists {
    	public class ListNode{
    		int val;
    		ListNode next=null;
    		public ListNode(int val) {
    			this.val=val;
    		}		
    	}
        
    	/*
    	 * 递归版本
    	 */
        public ListNode merge(ListNode list1,ListNode list2) {
        	if(list1==null)	return list2;
        	if(list2==null)	return list1;
        	if(list1.val<list2.val) {
        		list1.next=merge(list1.next, list2);
        		return list1;
        	}else {
        		list2.next=merge(list1, list2.next);
        		return list2;
        	}
        }
        
        /*
         * 非递归
         */
        public ListNode merge2(ListNode list1,ListNode list2) {
        	if(list1==null)	return list2;
        	if(list2==null)	return list1;
        	ListNode dummyHead=new ListNode(0);  //不能为null
        	ListNode p=dummyHead;
        	while(list1!=null && list2!=null){
                if(list1.val<list2.val){
                    p.next=list1;
                    list1=list1.next;
                }else{
                    p.next=list2;
                    list2=list2.next;
                }
                p=p.next;
            }
        	if(list1==null)
        		p.next=list2;
        	else
        		p.next=list1;
        	return dummyHead.next;
        }
    }
    

## **收获**

1.递归还是不够熟悉，第一反应想到的还是非递归实现。注意每次操作相同时，要立即考虑到可以采用递归来进行实现。

2.递归实现时，需要注意链接的问题。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)