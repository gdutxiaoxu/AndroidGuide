# 【Java】 剑指offer(47) 礼物的最大价值  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

在一个m×n的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向左或者向下移动一格直到到达棋盘的右下角。给定一个棋盘及其上面的礼物，请计算你最多能拿到多少价值的礼物？

## 思路

动态规划：定义f(i,j)为到达(i,j)位置格子时能拿到的礼物总和的最大值，则有：f(i,j)=max{f(i,j),f(i,j)}+values(i,j)。

同上道题一样，如果直接使用递归会产生大量的重复计算，因此，创建辅助的数组来保存中间计算结果。

辅助数组不用和m*n的二维数组一样大，只需要保存上一层的最大值就可以。代码中使用长度为列数n的一位数组作为辅助数组，注释部分为二维辅助数组。

_![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/1407330-20181113093715360-36843950.png)_

辅助数组只需要存 √ 的部分

**测试算例** ****

1.功能测试（多行多列，一行多列，多行一列，一行一列）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：在一个m×n的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值
    //（价值大于0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向左或
    //者向下移动一格直到到达棋盘的右下角。给定一个棋盘及其上面的礼物，请计
    //算你最多能拿到多少价值的礼物？
    
    public class MaxValueOfGifts {
    	public int maxValueOfGifts(int[][] values) {
    		if(values==null || values.length<=0 ||values[0].length<=0) 
    			return 0;
    		int rows=values.length;
    		int cols=values[0].length;
    //		int[][] maxValue=new int[rows][cols];
    		int[] maxValue=new int[cols];
    		for(int i=0;i<rows;i++) {
    			for(int j=0;j<cols;j++) {
    				int left=0;
    				int up=0;
    				if(i>0)
    //					up=maxValue[i-1][j];
    					up=maxValue[j];
    				if(j>0)
    //					left=maxValue[i][j-1];
    					left=maxValue[j-1];
    //				maxValue[i][j]=Math.max(up, left)+values[i][j];
    				maxValue[j]=Math.max(up, left)+values[i][j];
    			}
    		}
    //		return maxValue[rows-1][cols-1];
    		return maxValue[cols-1];
    	}
    }
    

## **收获**

1.动态规划问题，用公式来表示清楚。

2.动态规划如果有大量重复计算，可以用循环+辅助空间来提高效率。

2.这道题不用二维数组，只需要用一维数组作为辅助空间即可，以后遇到对中间结果的保存问题，看看能否优化辅助空间。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)