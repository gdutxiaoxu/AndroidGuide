# 【Java】 剑指offer(54) 二叉搜索树的第k个结点  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

给定一棵二叉搜索树，请找出其中的第k小的结点。

## 思路

设置全局变量index=0，对BST进行中序遍历，每遍历一个结点，index+1，当index=k时，该结点即为所求结点。

**测试算例** ****

1.功能测试（左斜树、右斜树、普通树）

2.边界值测试（k=1,k=结点数目）

3.特殊测试（null，k <=0，k>结点数目）

## **Java代码**

    
    
    //题目：给定一棵二叉搜索树，请找出其中的第k大的结点。
    
    public class KthNodeInBST {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
        int index=0;
        
        TreeNode KthNode(TreeNode pRoot, int k){
            TreeNode pNode = null;
            if(pRoot==null || k<=0)
                return pNode;
            pNode = getKthNode(pRoot,k);
            return pNode;
        }
        
        private TreeNode getKthNode(TreeNode pRoot, int k){
            TreeNode kthNode=null;
            
            if(pRoot.left!=null)
                kthNode=getKthNode(pRoot.left,k);
            
            if(kthNode==null){
                index++;
                if(k==index)
                    kthNode = pRoot;
            }
            
            if(kthNode==null && pRoot.right!=null)
                kthNode=getKthNode(pRoot.right,k);
            
            return kthNode;
        }
    }
    

## **收获**

1.熟练掌握二叉搜索树和中序遍历。

2.用中序遍历实现功能时，一定要注意返回值是否满足要求。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)