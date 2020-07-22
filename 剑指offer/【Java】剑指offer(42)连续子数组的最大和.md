# 【Java】 剑指offer(42) 连续子数组的最大和  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个整型数组，数组里有正数也有负数。数组中一个或连续的多个整/数组成一个子数组。求所有子数组的和的最大值。要求时间复杂度为O(n)。

## 思路

分析规律，从第一个数字开始累加，若走到某一个数字时，前面的累加和为负数，说明不能继续累加了，要从当前数字重新开始累加。在累加过程中，将每次累加和的最大值记录下来，遍历完成后，返回该数字。

**测试算例** ****

1.功能测试（输入数组有正有负，全负数，全正数）

2.特殊输入测试（null）

## **Java代码**

    
    
    //题目：输入一个整型数组，数组里有正数也有负数。数组中一个或连续的多个整
    //数组成一个子数组。求所有子数组的和的最大值。要求时间复杂度为O(n)。
    
    public class GreatestSumOfSubarrays {
        boolean InvalidInput = false;
        public int FindGreatestSumOfSubArray(int[] array) {
            if(array==null || array.length<=0){
                InvalidInput = true;
                return 0;
            }
            InvalidInput = false;
            int sum=array[0];
            int maxSum=array[0];
            for(int i=1;i<array.length;i++){
                if(sum<0)
                    sum=array[i];
                else
                    sum+=array[i];
                if(sum>maxSum)
                    maxSum=sum;
            }
            return maxSum;
        }
    }
    

## **收获**

1.复杂度要求为O(n)，考虑是否可以从头开始遍历，找规律。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)