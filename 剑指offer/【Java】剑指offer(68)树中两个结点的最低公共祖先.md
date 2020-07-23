# 【Java】 剑指offer(68) 树中两个结点的最低公共祖先  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入两个树结点，求它们的最低公共祖先。

## 思路

该题首先要和面试官确定是否为二叉树，得到肯定答复后，还要确定是否为二叉搜索树，是否有父指针，或者仅仅是普通二叉树。

1.树为二叉搜索树时，最低公共祖先结点的大小在两个树结点大小的中间。

2.树为普通树时，使用遍历将子结点的信息往上传递。在左右子树中进行查找是否存在两个树结点，如果两个树结点分别在左右子树上，说明该根结点就是它们的最低公共祖先。

**测试用例**

1.功能测试（普通树，左斜树，右斜树）

2.特殊测试（null）

## **Java代码**

    
    
    	/*
    	 * 二叉搜索树
    	 * 利用大小关系即可
    	 */
    	public TreeNode getLowestCommonParentBST(TreeNode root,TreeNode node1,TreeNode node2) {
    		while(true) {
    			if(root==null)
    				return root;
    			if(root.val<node1.val && root.val<node2.val)
    				root=root.right;
    			else if(root.val>node1.val && root.val>node2.val) 
    				root=root.right;
    			else 
    				return root;
    		}
    	}
    	
    
    	/*
    	 * 普通二叉树
    	 * 将下面结点的信息利用递归s往上传递
    	 */
    	public TreeNode getLowestCommonParent(TreeNode root,TreeNode node1,TreeNode node2) {
    		if(root==null || root== node1 || root== node2)
    			return root;
    		TreeNode left=getLowestCommonParent(root.left, node1, node2);
    		TreeNode right=getLowestCommonParent(root.right, node1, node2);
    		return left==null? right:right==null? left:root;
    	//	上面这句代码就是：
    	//	if(left==null) {
    	//			return right;
    	//	}else {
    	//		if(right==null)
    	//			return left;
    	//		else
    	//			return root;
    	//	}
    	}
    

## **收获**

1.《剑指OFFER》一书中的方法：普通二叉树时，可以采用链表来存储从根结点到两个树结点的路径，找出两条路径的最后公共结点，就是最低公共祖先。这个方法也要学会。

2.这里的方法根据特性：两个树结点分别在左右子树上时，该根结点就是最低公共祖先；非常方便，一定要掌握。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)