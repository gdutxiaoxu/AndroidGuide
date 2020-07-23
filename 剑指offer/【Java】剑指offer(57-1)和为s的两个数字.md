# 【Java】 剑指offer(57-1) 和为s的两个数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，输出任意一对即可。

## 思路

从头开始遍历数字，确定一个数字后，对后面的数字遍历，判断和是否为s，这种方法复杂度为O(n^2)，效率太低。

我们考虑到，如果一个数字比较小，那么另一个数字一定比较大，同时数字为递增排列；所以，我们设置两个指针，一个指针small从第一个数字（最小）出发，另一个指针big从最后一个数字（最大）出发：

当small加big的和小于s时，只需要将small指向后一个数字（更大），继续判断；

当small加big的和大于s时，只需要将big指向前一个数字（更小），继续判断；

当small加big的和等于s时，求解完成。

由于是从两边往中间移动，所以不会有跳过的情况，时间复杂度为 **O(n)** 。

**测试算例** ****

1.功能测试（存在/不存在和为s的一对数字）

2.特殊输入测试（null）

## **Java代码**

    
    
    //题目：输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们
    //的和正好是s。如果有多对数字的和等于s，输出任意一对即可。
    
    public class TwoNumbersWithSum {
        public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
            ArrayList<Integer> list = new ArrayList<Integer>();
            if(array==null || array.length<=0)
                return list;
            int low=0;
            int high=array.length-1;
            while(low<high){
                if(array[low]+array[high]==sum){
                    list.add(array[low]);
                    list.add(array[high]);
                    break;
                }else if(array[low]+array[high]<sum)
                    low++;
                else
                    high--;
            }
            return list;
        }
    }
    

## **收获**

1.利用两个指针从两端向中间扫描，要学会这种技巧。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)