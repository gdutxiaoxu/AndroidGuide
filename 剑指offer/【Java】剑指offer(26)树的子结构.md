# 【Java】 剑指offer(26) 树的子结构  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入两棵二叉树A和B，判断B是不是A的子结构。

## 思路

1）先对A树进行遍历，找到与B树的根结点值相同的结点R；

2）判断A树中以R为根结点的子树是否包含B树一样的结构。 **  
**

**测试算例** ****

1.功能测试（A、B为普通二叉树；B是或者不是A树的子结构）

2.特殊测试（任意一个或者两个树的根结点为null；左斜树；右斜树）

## **Java代码**

    
    
    //题目：输入两棵二叉树A和B，判断B是不是A的子结构。
    
    public class SubstructureInTree {
    	public class TreeNode{
    		double val;
    		TreeNode left = null;
    		TreeNode right =null;
    		public TreeNode(int val) {
    			this.val=val;
    		}
    	}
    	
    	/*
    	 * 主程序，对每个结点遍历判断
    	 */
        public boolean hasSubtree(TreeNode root1,TreeNode root2) {
            if(root1==null || root2==null)
            	return false;
    //        boolean result=false;
    //        if(equal(root1.val, root2.val)) {
    //        	result = doesTree1HasTree2(root1, root2);
    //        	if(!result)
    //        		result=hasSubtree(root1.left, root2)
    //        		||hasSubtree(root1.right, root2);
    //        }
    //        return result;
            //上面几行可以直接写成：
            return doesTree1HasTree2(root1, root2)|| hasSubtree(root1.left, root2)
            		||hasSubtree(root1.right, root2);
        }  
        
        /*
         * 判断root结点开始的子树中各个结点是否相同
         */
        private boolean doesTree1HasTree2(TreeNode root1,TreeNode root2) {
        	if(root2==null)	return true;  
        	if(root1==null)	return false;
        	return equal(root1.val, root2.val) && doesTree1HasTree2(root1.left, root2.left)
        			&& doesTree1HasTree2(root1.right, root2.right); 	
        }
    	
        /*
         * 判断两个浮点数是否相等
         */
        private boolean equal(double num1,double num2) {
        	if(num1-num2<0.0000001 && num1-num2>-0.0000001 )
        		return true;
        	return false;
        }   
    }
    

## **收获**

1.本题相当于对二叉树遍历的拓展，操作过程中，注意null的处理。

2.注意判断浮点数相等时有误差，不要直接用“==”判断。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)