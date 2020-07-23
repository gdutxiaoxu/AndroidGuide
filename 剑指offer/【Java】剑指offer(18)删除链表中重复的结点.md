# 【Java】 剑指offer(18) 删除链表中重复的结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

在一个排序的链表中，如何删除重复的结点？例如，在图3.4（a）中重复结点被删除之后，链表如图3.4（b）所示。

## 思路

设置一个preNode，用于记录当前结点的前一个结点，再设置一个布尔变量needDelete，如果当前结点和后一结点的值相同（记该值为dupVal），needDelete赋值为真。

当needDelete为真时，通过循环往后找到第一个不为dupVal的结点，把该结点设置为当前结点，并赋值给preNode.next，即相当于完成了删除操作；而当needDelete为假时，把当前结点和preNode往后移一位即可。

**测试算例**

1.功能测试（重复结点位于链表头部、中部、尾部，无重复结点）

2.特殊测试（null，所有结点均重复）

## **完整Java代码**

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
         public ListNode deleteDuplication(ListNode pHead){
            ListNode pre = null;
            ListNode cur = pHead;
            while(cur!=null){
                if(cur.next!=null && cur.next.val==cur.val){
                    while(cur.next!=null && cur.next.val==cur.val)
                        cur=cur.next;
                    cur=cur.next;
                    if(pre==null)
                        pHead=cur;
                    else
                        pre.next=cur;
                }else{
                    pre=cur;
                    cur=cur.next;
                }
            }
            return pHead;
        }

复习时写的

（含测试代码)

    
    
    package _18;
    
    /**
     * 
     * @Description 面试题18（二）：删除链表中重复的结点
     *
     * @author yongh
     * @date 2018年9月18日 下午6:30:53
     */
    
    // 题目：在一个排序的链表中，如何删除重复的结点？例如，在图3.4（a）中重复
    // 结点被删除之后，链表如图3.4（b）所示。
    
    public class DeleteDuplicatedNode {
    	class ListNode{
    		   int val;
    		    ListNode next = null;
    
    		    ListNode(int val,ListNode next) {
    		        this.val = val;
    		        this.next=next;
    		    }
    	}
        public ListNode deleteDuplication(ListNode pHead){
            if(pHead==null||pHead.next==null) //空结点或者仅一个结点
                return pHead;
            ListNode preNode = null;
            ListNode curNode = pHead;
            
            while(curNode!=null){
                boolean needDelete=false;
                if(curNode.next!=null && curNode.val==curNode.next.val)
                    needDelete=true;
                if(!needDelete){  //当前结点不重复
                    preNode=curNode;
                    curNode=curNode.next;
                }else{            //当前结点重复
                    int dupValue=curNode.val;
                    ListNode toBeDel = curNode;
                    while(toBeDel!=null&&toBeDel.val==dupValue){
                        //这里删除暂时不涉及前一结点操作，其实主要是找出后面第一个不重复结点
                        toBeDel = toBeDel.next;
                    }
                    if(preNode==null){  //说明删除的结点为头结点
                        pHead=toBeDel;
                    }else{
                        preNode.next=toBeDel;
                    }
                    curNode=toBeDel;  //这个结点还是可能会出现重复的，所以不能=next
                }
            }
            return pHead;
        }
    	
        
        //========测试代码======
    	void test(ListNode pHead) {
    		System.out.println("-----------");
    		System.out.print("The original list is: ");
    		ListNode curr=pHead;
    		if(curr!=null) {
    			while(curr.next!=null) {
    				System.out.print(curr.val+",");
    				curr=curr.next;
    			}
    			System.out.println(curr.val);
    		}else {
    			System.out.println();
    		}
    		pHead=deleteDuplication(pHead);
    		System.out.print("The result list is: ");
    		curr=pHead;
    		if(curr!=null) {
    			while(curr.next!=null) {
    				System.out.print(curr.val+",");
    				curr=curr.next;
    			}
    			System.out.println(curr.val);
    		}else {
    			System.out.println();
    		}
    		System.out.println("-----------");
    	}
        
    	
    	/**
    	 * 重复结点位于链表头部
    	 */
    	void test1() {
    		ListNode p4=new ListNode(3, null);
    		ListNode p3=new ListNode(2, p4);
    		ListNode p2=new ListNode(1, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 重复结点位于链表尾部
    	 */
    	void test2() {
    		ListNode p4=new ListNode(3, null);
    		ListNode p3=new ListNode(3, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 重复结点位于链表中部
    	 */
    	void test3() {
    		ListNode p4=new ListNode(3, null);
    		ListNode p3=new ListNode(2, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 连续出现重复结点
    	 */
    	void test4() {
    		ListNode p6=new ListNode(3, null);
    		ListNode p5=new ListNode(3, p6);
    		ListNode p4=new ListNode(2, p5);
    		ListNode p3=new ListNode(2, p4);
    		ListNode p2=new ListNode(1, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 多个重复结点
    	 */
    	void test5() {
    		ListNode p6=new ListNode(3, null);
    		ListNode p5=new ListNode(3, p6);
    		ListNode p4=new ListNode(3, p5);
    		ListNode p3=new ListNode(2, p4);
    		ListNode p2=new ListNode(1, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 无重复结点
    	 */
    	void test6() {
    		ListNode p6=new ListNode(6, null);
    		ListNode p5=new ListNode(5, p6);
    		ListNode p4=new ListNode(4, p5);
    		ListNode p3=new ListNode(3, p4);
    		ListNode p2=new ListNode(2, p3);
    		ListNode p1=new ListNode(1, p2);
    		test(p1);
    	}
    	
    	/**
    	 * 单个结点
    	 */
    	void test7() {
    		ListNode p1=new ListNode(6, null);
    		test(p1);
    	}
        
    	/**
    	 * null
    	 */
    	void test8() {
    		ListNode p1=null;
    		test(p1);
    	}
    	
    	public static void main(String[] args) {
    		DeleteDuplicatedNode demo= new DeleteDuplicatedNode();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    		demo.test7();
    		demo.test8();
    	}
        
    	
    	
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    -----------    The original list is: 1,1,2,3
    The result list is: 2,3
    -----------    -----------    The original list is: 1,2,3,3
    The result list is: 1,2
    -----------    -----------    The original list is: 1,2,2,3
    The result list is: 1,3
    -----------    -----------    The original list is: 1,1,2,2,3,3
    The result list is: 
    -----------    -----------    The original list is: 1,1,2,3,3,3
    The result list is: 2
    -----------    -----------    The original list is: 1,2,3,4,5,6
    The result list is: 1,2,3,4,5,6
    -----------    -----------    The original list is: 6
    The result list is: 6
    -----------    -----------    The original list is: 
    The result list is: 
    -----------
demo

## **收获**

1.删除多个结点时，只要把重复结点前一个结点的next指向重复结点的后一个结点；

2.不要把重复结点一个一个删除，先定义一个布尔变量确定当前结点是否重复，然后按上一句话的方法进行删除即可。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)