# 【Java】 剑指offer(7) 二叉树的下一个结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

_**更多《 剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**_

## 题目

给定一棵二叉树和其中的一个结点，如何找出中序遍历顺序的下一个结点？ 树中的结点除了有两个分别指向左右子结点的指针以外，还有一个指向父结点的指针。

## 思路

首先自己在草稿纸上画图，进行分析（不再展开）。可以发现下一个结点的规律为：

1.若当前结点有右子树时，其下一个结点为右子树中最左子结点；

2.若当前结点无右子树时，

（1）若当前结点为其父结点的左子结点时，其下一个结点为其父结点；

（2）若当前结点为其父结点的右子结点时，继续向上遍历父结点的父结点，直到找到一个结点是其父结点的左子结点（与（1）中判断相同），该结点即为下一结点。

**测试用例**

1.正常二叉树

2.左斜树、右斜树

4.单个结点

5.null

6.不同位置结点的下一结点（即上面分析的几种情况、无下一节点等情况）

## **完整 Java代码**

（含测试代码）

由于树的生成较为繁琐，下面不含全部测试代码，但主体代码已经通过了牛客网中的测试，可以保证没有问题。

    
    
    /**
     * 
     * @Description 二叉树的下一个结点 
     *
     * @author yongh
     * @date 2018年9月12日 下午7:20:45
     */
    
    // 题目：给定一棵二叉树和其中的一个结点，如何找出中序遍历顺序的下一个结点？
    // 树中的结点除了有两个分别指向左右子结点的指针以外，还有一个指向父结点的指针。
    
    public class NextNodeInBinaryTrees {
    	private class TreeLinkNode {
    		int val;
    		TreeLinkNode left = null;
    		TreeLinkNode right = null;
    		TreeLinkNode parent = null;
    
    		TreeLinkNode(int val) {
    			this.val = val;
    		}
    	}
    
    	public TreeLinkNode GetNext(TreeLinkNode pNode) {
    		if (pNode == null) {
    			System.out.print("结点为null ");
    			return null;
    		}
    		if (pNode.right != null) {
    			pNode = pNode.right;
                while(pNode.left!=null)
                    pNode=pNode.left;
                return pNode;
    		}
            while(pNode.parent !=null){
                if(pNode==pNode.parent .left)
                    return pNode.parent;
                pNode=pNode.parent;
            }
            return null;
    	}
    
    	
    	// ==================================测试代码==================================
    	//创建树较为繁琐，未包括所有测试代码。
    	public void test1() {
    		TreeLinkNode node = null;
    		TreeLinkNode nextNode = GetNext(node);
    		if(nextNode!=null)
    			System.out.println(nextNode.val);
    		else
    			System.out.println("无下一结点");
    	}
    
    	public void test2() {
    		TreeLinkNode node1 = new TreeLinkNode(1);
    		TreeLinkNode node2 = new TreeLinkNode(2);
    		TreeLinkNode node3 = new TreeLinkNode(3);
    		TreeLinkNode node4 = new TreeLinkNode(4);
    		node1.left = node2;
    		node1.right = node3;
    		node2.parent = node1;
    		node3.parent = node1;
    		node4.left=node1;
    		node1.parent=node4;
    		TreeLinkNode nextNodeOf1=GetNext(node1);
    		TreeLinkNode nextNodeOf2=GetNext(node2);
    		TreeLinkNode nextNodeOf3=GetNext(node3);
    		TreeLinkNode nextNodeOf4=GetNext(node4);
    		if(nextNodeOf1!=null)
    			System.out.println("1结点的下一个结点值为："+nextNodeOf1.val);
    		else
    			System.out.println("1结点无下一结点");
    		if(nextNodeOf2!=null)
    			System.out.println("2结点的下一个结点值为："+nextNodeOf2.val);
    		else
    			System.out.println("2结点无下一结点");
    		if(nextNodeOf3!=null)
    			System.out.println("3结点的下一个结点值为："+nextNodeOf3.val);
    		else
    			System.out.println("3结点无下一结点");
    		if(nextNodeOf4!=null)
    			System.out.println("4结点的下一个结点值为："+nextNodeOf4.val);
    		else
    			System.out.println("4结点无下一结点");
    	}
    	
    	public static void main(String[] args) {
    		NextNodeInBinaryTrees demo = new NextNodeInBinaryTrees();
    		System.out.print("test1:");
    		demo.test1();
    		System.out.print("test2:");
    		demo.test2();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    test1:结点为null 无下一结点
    test2:1结点的下一个结点值为：3
    2结点的下一个结点值为：1
    3结点的下一个结点值为：4
    4结点无下一结点

NextNodeInBinaryTrees

## **收获**

1.在面对复杂问题时要学会画图和举例分析

2.在分情况讨论时，一定要考虑到所有情况，这些都是在写代码前需要考虑到的。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)