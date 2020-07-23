# 【Java】 剑指offer(63) 股票的最大利润  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖交易该股票可能获得的利润是多少？例如一只股票在某些时间节点的价格为{9, 11, 8, 5,7,
12, 16, 14}。如果我们能在价格为5的时候买入并在价格为16时卖出，则能收获最大的利润11。

## 思路

遍历每一个数字，并保存之前最小的数字，两者差最大即为最大利润。 **  
**

值得注意的是，我自己一开始写的代码是默认不能亏本（即可以不买入卖出，利润不能为负数），所以比较简单；但如果可以亏本，最大利润指的是最小的亏损，那么要注意最小数字不能是最后一个。在下面的代码中可以注意比较两种情况的差别。可以考虑的例子如
{  16, 11, 7, 4, 2, 1 }

**测试算例** ****

1.功能测试（数组递增/递减/无序）

2.特殊测试（null，空数组）

3.边界值测试（数组仅两个数字）

## **Java代码**

    
    
    //题目：假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖交易该股
    //票可能获得的利润是多少？例如一只股票在某些时间节点的价格为{9, 11, 8, 5,
    //7, 12, 16, 14}。如果我们能在价格为5的时候买入并在价格为16时卖出，则能
    //收获最大的利润11。
    
    public class MaximalProfit {
    	public static int MaxDiff(int[] arr) {
    		if(arr==null || arr.length<2)
    			return -1;  //error
    		int min=arr[0];
    		
    		//最大利润可以是负数，只要亏损最小就行
    		int maxDiff=arr[1]-min;  
    		for(int i=1;i<arr.length;i++) {
    			if(arr[i-1]<min)     //保存“之前”最小数字
    				min=arr[i-1];   
    			if(arr[i]-min>maxDiff)
    				maxDiff=arr[i]-min;
    		}
    		
    		//默认不能亏本，代码简单，上面复杂的代码注意细节
    //		int maxDiff=0;  
    //		for(int i=1;i<arr.length;i++) {
    //			if(arr[i]<min)
    //				min=arr[i];
    //			else if(arr[i]-min>maxDiff)
    //				maxDiff=arr[i]-min;
    //		}
    		return maxDiff;
    	}
    	
    	
    	//简单快速测试下
    	public static void main(String[] args) {
    		int[] arr1=null;
    		System.out.println(MaxDiff(arr1)==-1);
    		
    		int[] arr2={  };
    		System.out.println(MaxDiff(arr2)==-1);
    		
    		int[] arr3={ 16, 16, 16, 16, 16 };
    		System.out.println(MaxDiff(arr3)==0);
    		
    		int[] arr4={ 1, 2, 4, 7, 11, 16 };
    		System.out.println(MaxDiff(arr4)==15);
    		
    		int[] arr5={  16, 11, 7, 4, 2, 1 };
    		System.out.println(MaxDiff(arr5)==-1);
    		
    		int[] arr6={ 9, 11, 5, 7, 16, 1, 4, 2 };
    		System.out.println(MaxDiff(arr6)==11);
    		
    		int[] arr7={ 2,4};
    		System.out.println(MaxDiff(arr7)==2);
    		
    		int[] arr8={ 4,2};
    		System.out.println(MaxDiff(arr8)==-2);	
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
     true
    true
    true
    true
    true
    true
    true
    true

MaximalProfit

## **收获**

1.蛮力法时间复杂度为O(n^2)，肯定不对。我们从头到尾遍历，确定规律。可以发现找出之前的最小值即可。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)