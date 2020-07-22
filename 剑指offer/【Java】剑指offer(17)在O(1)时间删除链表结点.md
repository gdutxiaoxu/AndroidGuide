# 【Java】 剑指offer(17) 在O(1)时间删除链表结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

给定单向链表的头指针和一个结点指针，定义一个函数在O(1)时间删除该结点。

## 思路

通常那样从头开始查找删除需要的时间为O(n)，要在O(1)时间删除某结点，可以这样实现：设待删除结点i的下一个结点为j，把j的值复制到i，再把i的指针指向j的下一个结点，最后删除j，效果就相当于删除j。

注意特殊情况：1.当待删除结点i为尾结点时，无下一个结点，则只能从头到尾顺序遍历；2.当链表中只有一个结点时（即是头结点，又是尾结点），必须把头结点也设置为null。

本题有个缺陷：要求O(1)时间删除，相当于隐藏了一个假设：待删除的结点的确在表中

**测试算例**

1.功能测试（多个结点链表，删除头结点、中间结点和尾结点；单个结点链表）

2.特殊测试（头结点或删除结点为null）

## **完整Java代码**

（含测试代码)

    
    
    package _18;
    /**
     * 
     * @Description 面试题18（一）：在O(1)时间删除链表结点
     *
     * @author yongh
     * @date 2018年9月18日 下午3:57:59
     */
    
    //题目：给定单向链表的头指针和一个结点指针，定义一个函数在O(1)时间删除该
    //结点。
    
    //注：本题存在缺陷，要求O(1)时间，则无法确定待删除结点的确在表中
    
    public class DeleteNodeInList {
    	public class ListNode{
    		int val;
    		ListNode next;
    		public ListNode(int value,ListNode nextNode) {
    			val=value;
    			next=nextNode;
    		}
    	}
    	
    	/**
    	 * 返回值：头结点
    	 * 返回值不可以为void，否则头结点无法删除
    	 * 即：函数中虽然令head=null，但返回到主程序后，
    	 * head还是不变，所以令该函数返回值为ListNode
    	 */
    	public ListNode deleteNode(ListNode head,ListNode pToBeDeleted) {
    		if(head==null||pToBeDeleted==null)
    			return head;
    		//待删除结点不是尾结点
    		if(pToBeDeleted.next!=null) {
    			ListNode nextNode=pToBeDeleted.next;
    			pToBeDeleted.val=nextNode.val;
    			pToBeDeleted.next=nextNode.next;
    			nextNode=null;
    		//只有一个结点（即是尾结点，又是头结点）
    		}else if(head==pToBeDeleted) {
    			pToBeDeleted=null;
    			head=null;
    		//链表含多个结点，删除尾结点
    		}else {
    			ListNode preNode=head;
    			while(preNode.next!=pToBeDeleted && preNode!=null) {
    				preNode=preNode.next;
    			}
    			if(preNode==null) {
    				System.out.println("无法找到待删除结点！");
    				return head;
    			}			
    			preNode.next=null;
    			pToBeDeleted=null;
    		}
    		return head;
    	}	
    	 
    	//=========测试代码==========
    	void test(ListNode head,ListNode PToBeDelete) {
    		System.out.println("============");
    		System.out.print("The original list is: ");
    		ListNode curr=head;
    		if(curr!=null) {
    			while(curr.next!=null) {
    				System.out.print(curr.val+",");
    				curr=curr.next;
    			}
    			System.out.println(curr.val);
    		}else {
    			System.out.println();
    		}
    		
    		System.out.print("The node to be deleted is: ");
    		if(PToBeDelete!=null)
    			System.out.println(PToBeDelete.val);
    		else
    			System.out.println();
    		
    		curr=deleteNode(head, PToBeDelete);		
    		System.out.print("The result list is: ");
    		if(curr!=null) {
    			while(curr.next!=null) {
    				System.out.print(curr.val+",");
    				curr=curr.next;
    			}
    			System.out.println(curr.val);
    		}else {
    			System.out.println();
    		}
    		System.out.println("============");
    	}
    	
    	/**
    	 * 链表含多个结点，删除头结点
    	 */
    	void test1() {
    		ListNode p4=new ListNode(4, null);
    		ListNode p3=new ListNode(3, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1, p1);
    	}
    	
    	/**
    	 * 链表含多个结点，删除中间结点
    	 */
    	void test2() {
    		ListNode p4=new ListNode(4, null);
    		ListNode p3=new ListNode(3, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1, p3);
    	}
    	
    	/**
    	 * 链表含多个结点，删除尾结点
    	 */
    	void test3() {
    		ListNode p4=new ListNode(4, null);
    		ListNode p3=new ListNode(3, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1, p4);
    	}
    	
    	/**
    	 * 链表含一个结点，删除结点
    	 */
    	void test4() {
    		ListNode p4=new ListNode(4, null);
    		test(p4, p4);
    	}
    	
    	/**
    	 * 链表为空
    	 */
    	void test5() {
    		test(null, null);
    	}
    		
    	public static void main(String[] args) {
    		DeleteNodeInList demo = new DeleteNodeInList();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    ============
    The original list is: 1,2,3,4
    The node to be deleted is: 1
    The result list is: 2,3,4
    ============
    ============
    The original list is: 1,2,3,4
    The node to be deleted is: 3
    The result list is: 1,2,4
    ============
    ============
    The original list is: 1,2,3,4
    The node to be deleted is: 4
    The result list is: 1,2,3
    ============
    ============
    The original list is: 4
    The node to be deleted is: 4
    The result list is: 
    ============
    ============
    The original list is: 
    The node to be deleted is: 
    The result list is: 
    ============

DeleteNodeInList

## **收获**

1.链表中删除结点的方法中，虽然直接令head=null了，但在主函数中的head还是不变，因此要令删除结点的返回值为ListNode，将返回值赋值给主函数中的head，这样才能实现真正的删除。

2.另一种情况可以令删除函数返回值为void，只是需要定义一个头结点head(1中的head相当于是第一个结点)，这个头结点中不存任何数据，仅仅起到指针的作用，第一个结点是头结点的下一个结点，通过对head.next操作，能够实现真正的删除。

3.和链表有关的特殊情况：头结点，尾结点，链表仅一个结点，null等。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)