# 【Java】 剑指offer(53-2) 0到n-1中缺失的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0到n-1之内。在范围0到n-1的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

## 思路

分析易知，数组形式如下：

![](https://img2018.cnblogs.com/blog/1407330/201811/1407330-20181114145612145-1558110605.png)

如果从头到尾依次比较值与小标是否相等，时间复杂度为O(n)，效率低。

由于是排序数组，我们继续考虑使用二分查找算法，结合上图可知：

当中间数字等于其下标时，我们在后半部分查找；

当中间数字不等于其下标时，

1）如果中间数字的前一个数字也不等于其下标，则在前半部分查找；

2）如果中间数字的前一个数字等于其下标，则说明中间数字的下标即为我们所要找的数字。

**测试算例** ****

1.功能测试（缺失数字位于数组开头、中间或者结尾）

2.边界值测试（数字只有0或1）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字
    //都在范围0到n-1之内。在范围0到n-1的n个数字中有且只有一个数字不在该数组
    //中，请找出这个数字。
    
    public class MissingNumber {
    	public int getMissingNumber(int[] arr) {
    		if(arr==null || arr.length<=0) 
    			return -1;
    		int low=0;
    		int high=arr.length-1;
    		while(low<=high) {
    			int mid=(low+high)>>1;
    			if(arr[mid]!=mid) {
    				if(mid==0 || arr[mid-1]==mid-1)
    					return mid;
    				high=mid-1;
    			}else {
    				low=mid+1;
    			}
    		}
    		return -1;
    	}
    }
    

## **收获**

1.53-3:https://www.cnblogs.com/yongh/p/9958138.html#_label3

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)