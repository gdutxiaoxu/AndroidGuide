# 【Java】 剑指offer(36) 二叉搜索树与双向链表  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

## 思路

二叉搜索树、排序链表，想到使用中序遍历。

要实现双向链表，必须知道当前结点的前一个结点。根据中序遍历可以知道，当遍历到根结点的时候，左子树已经转化成了一个排序的链表了，根结点的前一结点就是该链表的最后一个结点（这个结点必须记录下来，将遍历函数的返回值设置为该结点即可），链接根结点和前一个结点，此时链表最后一个结点就是根结点了。再处理右子树，遍历右子树，将右子树的最小结点与根结点链接起来即可。左右子树的转化采用递归即可。

大概思想再理一下：首先想一下中序遍历的大概代码结构（先处理左子树，再处理根结点，之后处理右子树），假设左子树处理完了，就要处理根结点，而根结点必须知道左子树的最大结点，所以要用函数返回值记录下来；之后处理右子树，右子树的最小结点（也用中序遍历得到）要和根结点链接。

注意搞清楚修改后的中序遍历函数的意义（见代码注释）

**测试算例** ****

1.功能测试（一个结点；左右斜树；完全二叉树；普通二叉树）

2.特殊测试（根结点为null）

## **Java代码**

    
    
    //题目：输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求
    //不能创建任何新的结点，只能调整树中结点指针的指向。
    
    public class ConvertBinarySearchTree {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
    	public TreeNode convert(TreeNode head) {
    		if(head==null)
    			return head;
    		TreeNode lastNodeInList=null;
    		lastNodeInList=convertHelper(head,lastNodeInList);
    		TreeNode firstNodeInList=lastNodeInList;
    		while(firstNodeInList.left!=null) {
    			firstNodeInList=firstNodeInList.left;
    		}	
    		return firstNodeInList;
    	}
    	
    	//将以node为根结点的树转化为排序链表，链表头部与lastNode链接，并返回最后一个结点
    	private TreeNode convertHelper(TreeNode node,TreeNode lastNode) {
    		//处理左子树，获得最大结点
    		if(node.left!=null)
    			lastNode=convertHelper(node.left, lastNode);
    		//链接最大结点和根结点
    		node.left=lastNode;
    		if(lastNode!=null)
    			lastNode.right=node;
    		//处理右子树
    		lastNode=node;
    		if(node.right!=null)
    			lastNode=convertHelper(node.right, lastNode);
    		return lastNode;
    	}
    }
    

上面的代码是参考《剑指OFFER》写的，下面的代码是复习时重新写过的，思路比较简洁一点。非递归方法的核心是中序遍历非递归实现:https://www.cnblogs.com/yongh/p/9629940.html#_label1。

    
    
    public class Solution {
    	/*
    	* 递归版本
    	* 1.已知函数返回的是转换好的双向链表头结点
    	* 2.左子树处理完后与根结点连接
    	* 3.右子树处理，也与根结点连接
    	* 4.最后返回头结点
    	*/
    	public TreeNode Convert(TreeNode root) {
    		if (root == null)
    			return root;
    		// 处理左子树,获得左子树链表的头结点
    		TreeNode left = Convert(root.left);
    		TreeNode p = left;
    		if (left != null) {
    			// 找到左子树链表的末尾结点
    			while (p.right != null)
    				p = p.right;
    			// 连接结点
    			p.right = root;
    			root.left = p;
    		}
    		// 处理右子树，获得右子树链表的头结点
    		TreeNode right = Convert(root.right);
    		// 连接结点
    		if (right != null) {
    			root.right = right;
    			right.left = root;
    		}
    		return left == null ? root : left;
    	}
    
    	/* 非递归版本
    	 * 1.利用非递归中序遍历来连接结点
    	 */
    	public TreeNode Convert1(TreeNode root) {
    		TreeNode head = null;
    		TreeNode pre = null;
    		LinkedList<TreeNode> stack = new LinkedList<>();
    		while (root != null || !stack.isEmpty()) {
    			// 把root当作指针使用
    			while (root != null) {
    				stack.push(root);
    				root = root.left;
    			}
    			TreeNode node = stack.pop();
    			if (head == null) {
    				head = node;
    				pre = node;
    			} else {
    				node.left = pre;
    				pre.right = node;
    				pre = node; // 别漏写了
    			}
    			root = node.right;
    		}
    		return head;
    	}
    }
    

## **收获**

题目较复杂时，不要慌。这道题和中序遍历有关，把树分为三部分：根结点、左子树和右子树，思考在中序遍历中根结点应该如何处理，这是关键——要将左子树的最大结点、根结点、右子树的最小结点链接起来。左右子树的处理是相同的，因此采用递归。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)