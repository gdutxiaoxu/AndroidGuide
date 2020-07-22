# 【Java】 剑指offer(55-1) 二叉树的深度  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一棵二叉树的根结点，求该树的深度。从根结点到叶结点依次经过的/结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

## 思路

简洁理解：

树的深度=max(左子树深度，右子树深度)+1，采用递归实现。

**测试算例** ****

1.功能测试（左斜树、右斜树、普通树）

2.边界值测试（一个结点）

3.特殊测试（null）

## **Java代码**

    
    
    //题目：输入一棵二叉树的根结点，求该树的深度。从根结点到叶结点依次经过的
    //结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。
    
    public class TreeDepth {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
        public int TreeDepth(TreeNode root) {
            if(root==null)
                return 0;
            int left=TreeDepth(root.left);
            int right=TreeDepth(root.right);
            return Math.max(left+1,right+1);
        }
    }
    

## **收获**

1.深度从递归的角度理解，很赞，要记住。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)