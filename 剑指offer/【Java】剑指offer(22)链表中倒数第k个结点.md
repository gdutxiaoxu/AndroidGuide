# 【Java】 剑指offer(22) 链表中倒数第k个结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

**正文**

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个链表，输出该链表中倒数第k个结点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾结点是倒数第1个结点。例如一个链表有6个结点，从头结点开始它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个结点是值为4的结点。

## 思路

第一直觉是先从头开始遍历，计算链表个数n，然后重新遍历，第n-k+1个结点即为所需要的结点。但是需要遍历2次。后面采用了栈进行实现该方法，空间复杂度比较大。书中的方法则是：设置两个指针，第一个指针先遍历k-1步；从第k步开始，第二个指针指向头结点，两个结点同时往后遍历，当第一个指针到达最后一个结点时，第二个指针指向的正好是倒数第k个结点。（其实感觉还是近似遍历了两次啊。。）

**测试算例** ****

1.功能测试（第k个结点分别在链表的中间，头结点和尾结点）

2.特殊测试（头结点为null，k超出范围）

## **完整Java代码**

（含测试代码)

    
    
    package _22;
    
    import java.util.Stack;
    
    /**
     * 
     * @Description 面试题22：链表中倒数第k个结点
     *
     * @author yongh
     * @date 2018年10月14日 下午4:23:32
     */
    
    //题目：输入一个链表，输出该链表中倒数第k个结点。为了符合大多数人的习惯，
    //本题从1开始计数，即链表的尾结点是倒数第1个结点。例如一个链表有6个结点，
    //从头结点开始它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个结点是
    //值为4的结点。
    
    public class KthNodeFromEnd {
    	public static class ListNode {
    	    int val;
    	    ListNode next = null;
    	    ListNode(int val) {
    	        this.val = val;
    	    }
    
    	}
    	    
        //方法1：利用栈
        public ListNode FindKthToTail1(ListNode head,int k) {
            if(head==null || k<=0)
                return null;
            int numbOfList=1;
            Stack<ListNode> st = new Stack<ListNode>();
            st.push(head);
            ListNode node=head.next;
            while(node!=null){
                numbOfList++;
                st.push(node);
                node=node.next; 
            }
            if(k>numbOfList)
                return null;
            else{
                for(int i=1;i<=k;i++){
                    node=st.pop();
                }
                return node;
            }
        }
        
        //方法2：利用两个相距为k-1的指针
        public ListNode FindKthToTail2(ListNode head,int k) {
            if(head==null || k<=0)
                return null;
            ListNode pAhead=head;
            for(int i=1;i<k;i++){
                pAhead=pAhead.next;
                if(pAhead==null)
                	return null; 
            }
            ListNode pBehind = head;
            while(pAhead.next!=null) {
            	pAhead=pAhead.next;
            	pBehind=pBehind.next;
            }
            return pBehind;
        }
        
        //=====================测试代码=======================
        
        /*
         * null
         */
        void test1() {
        	ListNode head=null;
        	ListNode result=FindKthToTail2(head, 1);
        	if(result==null)
        		System.out.println("test1 passed!");
        	else
        		System.out.println("test1 failed!");   	
        }
        
        /*
         * k超出范围
         */
        void test2() {
        	ListNode head=new ListNode(2);
        	ListNode result=FindKthToTail2(head, 2);
        	if(result==null)
        		System.out.println("test2 passed!");
        	else
        		System.out.println("test2 failed!");   	
        }
        
        /*
         * 单个结点
         */
        void test3() {
        	ListNode head=new ListNode(1);
        	ListNode result=FindKthToTail2(head, 1);
        	if(result.val==1)
        		System.out.println("test3 passed!");
        	else
        		System.out.println("test3 failed!");   	
        }
        
        /*
         * 尾结点
         */
        void test4() {
        	ListNode node1=new ListNode(1);
        	ListNode node2=new ListNode(2);
        	ListNode node3=new ListNode(3);
        	ListNode node4=new ListNode(4);
        	node1.next=node2;
        	node2.next=node3;
        	node3.next=node4;
        	ListNode result=FindKthToTail2(node1, 1);
        	if(result.val==4)
        		System.out.println("test4 passed!");
        	else
        		System.out.println("test4 failed!");   	
        }
        
        /*
         * 中间结点
         */
        void test5() {
        	ListNode node1=new ListNode(1);
        	ListNode node2=new ListNode(2);
        	ListNode node3=new ListNode(3);
        	ListNode node4=new ListNode(4);
        	node1.next=node2;
        	node2.next=node3;
        	node3.next=node4;
        	ListNode result=FindKthToTail2(node1, 2);
        	if(result.val==3)
        		System.out.println("test5 passed!");
        	else
        		System.out.println("test5 failed!");   	
        }
        
        /*
         * 头结点
         */
        void test6() {
        	ListNode node1=new ListNode(1);
        	ListNode node2=new ListNode(2);
        	ListNode node3=new ListNode(3);
        	ListNode node4=new ListNode(4);
        	node1.next=node2;
        	node2.next=node3;
        	node3.next=node4;
        	ListNode result=FindKthToTail2(node1, 4);
        	if(result.val==1)
        		System.out.println("test6 passed!");
        	else
        		System.out.println("test6 failed!");   	
        }
        
        public static void main(String[] args) {
    		KthNodeFromEnd demo = new KthNodeFromEnd();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    test1 passed!
    test2 passed!
    test3 passed!
    test4 passed!
    test5 passed!
    test6 passed!

KthNodeFromEnd

## **收获**

1.注意代码的鲁棒性，开始思考前都需要注意特殊输入测试；

2.一个指针遍历链表无法解决问题时，可以考虑使用两个指针来遍历链表：两个指针 **先后遍历** （即该题目）、或者两个指针 **遍历速度不同**
（如：求链表中的中间结点，可以令一个指针一次走一步，另一个指针一次走两步来实现）

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)