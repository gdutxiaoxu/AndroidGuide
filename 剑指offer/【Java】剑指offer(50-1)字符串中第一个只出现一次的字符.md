# 【Java】 剑指offer(50-1) 字符串中第一个只出现一次的字符  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

在字符串中找出第一个只出现一次的字符。如输入"abaccdeff"，则输出'b'。

## 思路

创建哈希表，键值key为字符，值value为出现次数。第一遍扫描：对每个扫描到的字符的次数加一；第二遍扫描：对每个扫描到的字符通过哈希表查询次数，第一个次数为1的字符即为符合要求的输出。

由于字符（char）是长度为8的数据类型，共有256中可能，因此哈希表可以用一个长度为256的数组来代替，数组的下标相当于键值key，对应字符的ASCII码值；数组的值相当于哈希表的值value，用于存放对应字符出现的次数。

**测试算例** ****

1.功能测试（存在/不存在只出现一次的字符；全部都为只出现一次的字符）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：在字符串中找出第一个只出现一次的字符。如输入"abaccdeff"，则输出
    //'b'。
    
    public class FirstNotRepeatingChar {
    	public char firstNotRepeatingChar(String str) {
    		if(str==null)
    			return '\0';
    		int[] repetitions = new int[256];
    		for(int i=0;i<256;i++)
    			repetitions[i]=0;
    		for(int i=0;i<str.length();i++) {
    			int loc=(int) str.charAt(i);
    			repetitions[loc]+=1;
    		}
    		for(int i=0;i<str.length();i++) {
    			int loc=(int) str.charAt(i);
    			if(repetitions[loc]==1)
    				return (char)loc;
    		}
    		return '\0';
    	}
    	
    	public static void main(String[] args) {
    		FirstNotRepeatingChar demo =new FirstNotRepeatingChar();
    		System.out.println((demo.firstNotRepeatingChar("google")=='l'));
    		System.out.println((demo.firstNotRepeatingChar("aabccdbd")=='\0'));
    		System.out.println((demo.firstNotRepeatingChar("$abcdefg")=='$'));
    		System.out.println((demo.firstNotRepeatingChar(null)=='\0'));
    	}
    }
    

## **收获**

1.如果需要创建哈希表，键值为 字符，值为 数字时，可以考虑用数组（length=256）来替代，数组下标表示为字符的ASCII码值。

2.哈希表的时间复杂度为O(1)，要求有较高的查找速度时，可以考虑使用哈希表（Java中可以使用HashMap)

3.如果需要判断多个字符是否在某个字符串中出现过，或者统计多个字符在某个字符串中出现的次数，可以考虑基于数组创建一个简单的哈希表，这样可以用很小的空间消耗换来时间效率的提升。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)