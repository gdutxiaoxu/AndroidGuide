# 【Java】 剑指offer(27) 二叉树的镜像  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

## 思路

画图可以很清晰地得到思路：先前序遍历，对每个结点交换左右子结点。

**测试算例** ****

1.功能测试（普通二叉树；左斜树；右斜树；一个结点）

2.特殊测试（根结点为null；）

## **Java代码**

    
    
    //题目：请完成一个函数，输入一个二叉树，该函数输出它的镜像。
    
    public class MirrorOfBinaryTree {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
        public void Mirror(TreeNode root) {
            if(root==null)
            	return;
            //左右子结点交换
            TreeNode tempNode = root.left;
            root.left=root.right;
            root.right=tempNode;  	
    
            Mirror(root.left);
            Mirror(root.right);
        }
    }
    

## **收获**

画图使抽象问题形象化，面试时要在编程前先用画图、举例子等来解释思路。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)