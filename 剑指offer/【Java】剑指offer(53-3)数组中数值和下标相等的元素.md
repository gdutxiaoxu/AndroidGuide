# 【Java】 剑指offer(53-3) 数组中数值和下标相等的元素  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

假设一个单调递增的数组里的每个元素都是整数并且是唯一的。请编程实现一个函数找出数组中任意一个数值等于其下标的元素。例如，在数组{-3, -1,1, 3,
5}中，数字3和它的下标相等。

## 思路

53-1](https://www.cnblogs.com/yongh/p/9957949.html)和[53-2:https://www.cnblogs.com/yongh/p/9958093.html一样，不再从头到尾遍历，由于是排序数组，我们继续考虑使用二分查找算法：

1）当中间数字等于其下标时，中间数字即为所求数字；

2）当中间数字大于其下标时，在左半部分区域寻找；

2）当中间数字小于其下标时，在右半部分区域寻找；

**测试算例** ****

1.功能测试（包含/不包含与下标相等的数字）

2.边界值测试（数字位于数组开头、中间或者结尾；仅一个数字数组）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：假设一个单调递增的数组里的每个元素都是整数并且是唯一的。请编程实
    //现一个函数找出数组中任意一个数值等于其下标的元素。例如，在数组{-3, -1,
    //1, 3, 5}中，数字3和它的下标相等。
    
    public class IntegerIdenticalToIndex {
    	public int getNumberSameAsIndex(int[] arr) {
    		if(arr==null || arr.length<=0)
    			return -1;  //代表错误
    		int low=0;
    		int high=arr.length-1;
    		while(low<=high) {
    			int mid= (high+low)>>1;
    			if(arr[mid]>mid)
    				high=mid-1;
    			else if(arr[mid]<mid)
    				low=mid+1;
    			else 
    				return mid;
    		}
    		return -1;
    	}
    }
    

## **收获**

1.对于在 **排序数组** 中查找某些特定的数字，可以对二分法稍加改造，实现所需的功能。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)