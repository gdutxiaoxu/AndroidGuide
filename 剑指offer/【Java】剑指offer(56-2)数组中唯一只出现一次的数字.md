# 【Java】 剑指offer(56-2) 数组中唯一只出现一次的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

在一个数组中除了一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

## 思路

这道题中数字出现了三次，无法像[56-1)
数组中只出现一次的两个数字](https://www.cnblogs.com/yongh/p/9960018.html)一样通过利用异或位运算进行消除相同个数字。但是仍然可以沿用位运算的思路。

将所有数字的二进制表示的对应位都加起来，如果某一位能被三整除，那么只出现一次的数字在该位为0；反之，为1。

**测试算例** ****

1.功能测试（唯一出现的数字是0，正数，负数；重复出现的数字是0，正数，负数）

## **Java代码**

    
    
    //题目：在一个数组中除了一个数字只出现一次之外，其他数字都出现了三次。请
    //找出那个只出现一次的数字。
    
    public class NumberAppearingOnce {
    	public static int findNumberAppearingOnce(int[] arr) {
    		if(arr==null || arr.length<=0)
    			throw new RuntimeException();
    		int[] bitSum = new int[32];
    		for(int i=0;i<32;i++) 
    			bitSum[i]=0;
    		for(int i=0;i<arr.length;i++) {
    			int bitMask=1;
    			for(int j=31;j>=0;j--) {
    				int bit=arr[i]&bitMask;  //注意arr[i]&bitMask不一定等于1或者0，有可能等于00010000
    				if(bit!=0)
    					bitSum[j]+=1;
    				bitMask=bitMask<<1;
    			}
    		}
    		int result=0;
    		for(int i=0;i<32;i++) {
    			result=result<<1;
    			result+=(bitSum[i]%3);
    			//result=result<<1;  //不能放在后面，否则最前面一位就没了
    		}
    		return result;
    	}
    }
    

## **收获**

1.判断某个数x的第n位（如第3位）上是否为1，

1）通过 x &00000100 的结果是否为0 来判断。（不能根据是否等于1来判断）

2）通过（x>>3)&1 是否为0 来判断

2.通过number&bitMask的结果是否为0（不能用1判断），bitMask=1不断左移，可以将一个数的二进制存储到32位的数组中。

    
    
    	int number=100;
    	int bitMask=1;
    	for(int j=31;j>=0;j--) {
    		int bit=number&bitMask;  //注意arr[i]&bitMask不一定等于1或者0，有可能等于00010000
    		if(bit!=0)
    			bits[j]=1;
    		bitMask=bitMask<<1;
    	}

3.通过以下代码实现二进制转化为数字（注意左移语句的位置）：

    
    
    	int result=0;
    	for(int i=0;i<32;i++) {
    		result=result<<1;
    		result+=bits[i];
    		//result=result<<1;  //不能放在后面，否则最前面一位就没了
    	}
    

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)