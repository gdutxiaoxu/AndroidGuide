# 【Java】 剑指offer(52) 两个链表的第一个公共结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入两个链表，找出它们的第一个公共结点。

## 思路

蛮力法：遍历第一个链表的结点，每到一个结点，就在第二个链表上遍历每个结点，判断是否相等。时间复杂度为O(m*n)，效率低；

使用栈：由于公共结点出现在尾部，所以用两个栈分别放入两个链表中的结点，从尾结点开始出栈比较。时间复杂度O(m+n)，空间复杂度O(m+n)。

利用长度关系：计算两个链表的长度之差，长链表先走相差的步数，之后长短链表同时遍历，找到的第一个相同的结点就是第一个公共结点。

利用两个指针：一个指针顺序遍历list1和list2，另一个指针顺序遍历list2和list1，（这样两指针能够保证最终同时走到尾结点），两个指针找到的第一个相同结点就是第一个公共结点。

**测试算例** ****

1.功能测试（有/无公共结点；公共结点分别在链表的中间，头结点和尾结点）

2.特殊测试（头结点为null）

## **完整Java代码**

    
    
    //题目：输入两个链表，找出它们的第一个公共结点。
    
    public class FirstCommonNodesInLists {
    	public class ListNode{
    	    int val;
    	    ListNode next = null;
    	    ListNode(int val) {
    	        this.val = val;
    	    }
    	}
        
        //方法1：利用长度关系
        public ListNode findFirstCommonNode1(ListNode pHead1, ListNode pHead2) {
            int length1 = getLength(pHead1);
            int length2 = getLength(pHead2);
            int lengthDif = length1-length2;
            ListNode longList = pHead1;
            ListNode shortList = pHead2;
            if(lengthDif<0){
                longList = pHead2;
                shortList = pHead1;
                lengthDif = -lengthDif;
            }
            for(int i=0;i<lengthDif;i++)
                longList = longList.next;
            while(longList!=null && longList!=shortList ){
                longList=longList.next;
                shortList=shortList.next;
            }
            return longList;  //没有公共结点刚好是null
        }
        
        private int getLength(ListNode head){
            int len=0;
            while(head!=null){
                len++;
                head=head.next;
            }
            return len;
        }
    
        //方法2：两个指针，p1顺序遍历list1和list2；p2顺序遍历list2和list1；最终一定会相遇
        public ListNode findFirstCommonNode2(ListNode pHead1, ListNode pHead2) {
            ListNode p1=pHead1;
            ListNode p2=pHead2;
            while(p1!=p2){
                p1= p1==null ? pHead2 : p1.next;
                p2= p2==null ? pHead1 : p2.next;
            }
            return p1;
        }
    }
    

## **收获**

1.由于有共同结点时，后面的链表是重合的，所以这道题关键是要保证最后同时遍历到达尾结点，因此就有了后面三种方法：

利用栈的先进后出实现同时到达；

利用长度关系，长链表先行几步，实现同时到达；

两个指针同时遍历两个链表，一个先list1后list2，另一个则相反，也可以实现同时到达。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)