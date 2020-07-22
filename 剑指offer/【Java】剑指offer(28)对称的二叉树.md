# 【Java】 剑指offer(28) 对称的二叉树  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

## 思路

还是画图分析，不用分析根结点，只需要分析左右子树。可以看出，左右子树刚好是呈镜像的两颗二叉树，所以：对左子树采用（父-左-右）的前序遍历，右子树采用（父-右-左）的前序遍历，遍历时判断两个结点位置的值是否相等即可。（也可以这样理解：左树的左子树等于右树的右子树，左树的右子树等于右树的左子树，对应位置刚好相反，判断两子树相反位置上的值是否相等即可）

**测试算例** ****

1.功能测试（对称二叉树；结构不对称二叉树；结构对称但值不对称二叉树）

2.特殊测试（根结点为null；单个结点；所有结点的值都相等的二叉树）

## **Java代码**

    
    
    //题目：请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和
    //它的镜像一样，那么它是对称的。
    
    public class SymmetricalBinaryTree {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    	    public TreeNode(int val) {
    	        this.val = val;
    
    	    }
    	}
    	
        public boolean isSymmetrical(TreeNode pRoot){
            if(pRoot==null)
            	return true; //根结点为null时，认为是对称二叉树
            return isEqual(pRoot.left,pRoot.right);
        }
        
        private boolean isEqual(TreeNode pRoot1,TreeNode pRoot2){
        	if(pRoot1==null && pRoot2==null)
        		return true;
        	if(pRoot1==null || pRoot2==null)
        		return false;
        	return pRoot1.val==pRoot2.val 
        			&& isEqual(pRoot1.left, pRoot2.right)
        			&& isEqual(pRoot1.right, pRoot2.left);    	
        }
    }
    

## **收获**

画图使抽象问题形象化，本题还是相当于对数的遍历算法的理解。

这道题主要突破点在于看出左右两个子树数值刚好呈镜像，相反位置对比即可。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)