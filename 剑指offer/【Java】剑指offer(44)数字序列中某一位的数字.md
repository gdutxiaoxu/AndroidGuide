# 【Java】 剑指offer(44) 数字序列中某一位的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从0开始计数）是5，第13位是1，第19位是4，等等。请写一个函数求任意位对应的数字。

## 思路

逐一枚举数字，计算每个数字的位数相加，效率太低。

观察规律：

个位数的个数一共有10个，即0~9，共占了10*1位数字；

两位数的个数一共有90个，即10~99，每个数字占两位，共占了90*2位数字；

……

m位数的个数一共有9*10^(m-1)个，每个数字占m位，占了9*10^(m-1)*m位数字。

判断第n个对的数字是属于几位数，再从几位数中进行寻找。

**测试算例** ****

1.功能测试（输入19、1000等）

2.边界值测试（输入0、1等）

## **Java代码**

    
    
    //题目：数字以0123456789101112131415…的格式序列化到一个字符序列中。在这
    //个序列中，第5位（从0开始计数）是5，第13位是1，第19位是4，等等。请写一
    //个函数求任意位对应的数字。
    
    public class DigitsInSequenc {
    	public int digitAtIndex(int index) {
    		if(index<0)
    			return -1;
    		int m=1;  //m位数
    		while(true) {
    			int numbers=numbersOfIntegers(m);  //m位数的个数
    			if(index<numbers*m) 
    				return getDigit(index,m);  
    			index-=numbers*m;
    			m++;
    		}
    	}
    	
    	/*
    	 * 返回m位数的总个数
    	 * 例如，两位数一共有90个：10~99；三位数有900个：100~999
    	 */
    	private int numbersOfIntegers(int m) {
    		if(m==1)
    			return 10;
    		return (int) (9*Math.pow(10, m-1));
    	}
    	
    	/*
    	 * 获取数字
    	 */
    	private int getDigit(int index, int m) {
    		int number=getFirstNumber(m)+index/m;  //对应的m位数
    		int indexFromRight = m-index%m;  //在数字中的位置
    		for(int i=1;i<indexFromRight;i++) 
    			number/=10;
    		return number%10;
    	}
    	
    	/*
    	 * 第一个m位数
    	 * 例如第一个两位数是10，第一个三位数是100
    	 */
    	private int getFirstNumber(int m) {
    		if(m==1)
    			return 0;
    		return (int) Math.pow(10, m-1);
    	}
    
    	public static void main(String[] args) {
    		DigitsInSequenc demo=new DigitsInSequenc();
    		System.out.println(demo.digitAtIndex(0)==0); 
    		System.out.println(demo.digitAtIndex(1)==1); 
    		System.out.println(demo.digitAtIndex(19)==4); 
    		System.out.println(demo.digitAtIndex(1000)==3); 
    		System.out.println(demo.digitAtIndex(1001)==7); 
    		System.out.println(demo.digitAtIndex(1002)==0); 
    	}
    }
    

## **收获**

1.程序逻辑要整理清楚，细节要注意

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)