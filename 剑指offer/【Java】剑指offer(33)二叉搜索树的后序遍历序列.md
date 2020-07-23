# 【Java】 剑指offer(33) 二叉搜索树的后序遍历序列  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则返回true，否则返回false。假设输入的数组的任意两个数字都互不相同。

## 思路

二叉树后序遍历数组的最后一个数为根结点，剩余数字中，小于根结点的数字（即左子树部分）都排在前面，大于根结点的数字（即右子树部分）都排在后面。根据遍历数组的这个特性，可以编写出一个递归函数，用于实现题目所要求的判断功能。

**测试算例** ****

1.功能测试（左斜树；右斜树；能对应的二叉树；不能对应的二叉树序列）

2.特殊测试（null；一个结点）

## **Java代码**

    
    
    //题目：输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。
    //如果是则返回true，否则返回false。假设输入的数组的任意两个数字都互不相同。
    
    public class SquenceOfBST {
    	public boolean  verifySquenceOfBST(int[] sequence) {
    		if(sequence== null || sequence.length<=0)
    			return false;
    		return verifyCore(sequence, 0, sequence.length-1);
    	}
    		
    	private boolean verifyCore(int[] sequence,int start,int end) {
    		if(start>=end) 
    			return true;
    		//判断左子树
    		int mid=start;
    		while(sequence[mid]<sequence[end]) 
    			mid++;
    		//判断右子树
    		for(int i=mid;i<end;i++) {
    			if(sequence[i]<sequence[end])
    				return false;
    		}
    		return verifyCore(sequence, start, mid-1)&&verifyCore(sequence, mid, end-1);
    	}	
    }
    

## **收获**

1.寻找出序列规律，就能较快得到思路。此题如果改为BST的前序遍历也是相同的思路。

2.对于要求处理二叉树序列的问题：找到根结点后，拆分出左右子树，对左右子树可以进行递归处理。

3.虽然有了思路，但自己在编写代码的时候还是写得比较乱，花了一些时间才能修改出比较简洁和清晰易懂的版本，说明自己写的代码量还是不够，要继续多加练习。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)