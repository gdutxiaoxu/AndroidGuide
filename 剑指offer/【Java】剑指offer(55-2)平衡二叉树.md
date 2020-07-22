# 【Java】 剑指offer(55-2) 平衡二叉树  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一棵二叉树的根结点，判断该树是不是平衡二叉树。如果某二叉树中任意结点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

## 思路

在[(55-1)
二叉树的深度](https://www.cnblogs.com/yongh/p/9958736.html)基础上修改：计算树的深度，树的深度=max(左子树深度，右子树深度)+1。在遍历过程中，判断左右子树深度相差是否超过1，如果不平衡，则令树的深度=-1，用来表示树不平衡。最终根据树的深度是否等于-1来确定是否为平衡树。

**测试算例** ****

1.功能测试（左斜树、右斜树、平衡或者不平衡树）

3.特殊测试（一个结点，null）

## **Java代码**

    
    
    //题目：输入一棵二叉树的根结点，判断该树是不是平衡二叉树。如果某二叉树中
    //任意结点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。
    
    public class BalancedBinaryTree {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
        public boolean IsBalanced_Solution(TreeNode root) {
            return getDepth(root)!=-1;
        }
        
        public int getDepth(TreeNode root) {
            if(root==null)    return 0;
            int left=getDepth(root.left);
            if(left==-1)    return -1;
            int right=getDepth(root.right);
            if(right==-1)    return -1;
            return Math.abs(left - right) > 1 ? -1 : 1 + Math.max(left, right);
        }
        
        /*
        //自己开始想的方法，但是一定要把树给遍历完才行；上面的方法实现了剪枝
        boolean isBalanced=true;
        public boolean IsBalanced_Solution(TreeNode root) {
            TreeDepth(root);
            return isBalanced;
        }
         
        public int TreeDepth(TreeNode root) {
            if(root==null)
                return 0;
            int left=TreeDepth(root.left);
            int right=TreeDepth(root.right);
            if(left-right>1 || right-left>1)
                isBalanced=false;
            return Math.max(left+1,right+1);
        }
        */
    }
    

## **收获**

1.在判断出树不平衡后，进行剪枝（即代码中直接返回-1，不再对其他子树进行判断），以提高效率。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)