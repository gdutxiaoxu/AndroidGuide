# 【Java】 剑指offer(50-2) 字符流中第一个只出现一次的字符  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是'g'。当从该字符流中读出前六个字符"google"时，第一个只出现一次的字符是'l'。

## 思路

字符只能一个一个从字符流中读出来，因此要定义一个容器来保存字符以及其在字符流中的位置。

为尽可能搞笑解决问题，要在O(1)时间内往数据容器中插入字符，及其对应的位置，因此这个数据容器可以用哈希表来实现，以字符的ASCII码作为哈希表的键值key，字符对应的位置作为哈希表的值value。

开始时，哈希表的值都初始化为-1，当读取到某个字符时，将位置存入value中，如果之前读取过该字符（即value
>=0），将value赋值为-2，代表重复出现过。最后对哈希表遍历，在value>=0的键值对中找到最小的value，该value即为第一个只出现一次的字符，ASCII码为key的字符即为所求字符。

**测试算例** ****

1.功能测试（读入一个字符；读入多个字符；所有字符都唯一；所有字符重复）

2.特殊测试（读入0个字符）

## **Java代码**

    
    
    //题目：请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从
    //字符流中只读出前两个字符"go"时，第一个只出现一次的字符是'g'。当从该字
    //符流中读出前六个字符"google"时，第一个只出现一次的字符是'l'。
    
    public class FirstCharacterInStream {
    	private int index;
    	private int[] occurence;
    	
    	public FirstCharacterInStream() {  //在构造函数中初始化成员变量
    		index=0;
    		occurence = new int[256];
    		for(int i=0;i<256;i++) {
    			occurence[i]=-1;
    		}
    	}
    	
    	public void insert(char ch) {
    		if(occurence[(int)ch]==-1) {
    			occurence[(int)ch]=index;   //第一次出现
    		}else if(occurence[(int)ch]>=0) {
    			occurence[(int)ch]=-2;   //已经出现过了
    		}
    		index++;
    	}
    	
    	public char getFirst() {
    		int minIndex=Integer.MAX_VALUE;  //最大的integer
    		char ch='#';
    		for(int i=0;i<256;i++) {
    			if(occurence[i]>=0 && occurence[i]<minIndex) {
    				ch = (char) i;
    				minIndex=occurence[i];
    			}
    		}
    		return ch;
    	}
    }

## **收获**

1.对于数据流、字符流等，需要定义数据容器来保存记录。

流和串的区别：

1）串：字符串已经保存下来了，能够读取遍历，因此在[字符串中第一个只出现一次的字符](https://www.cnblogs.com/yongh/p/9954083.html
"发布于2018-11-13 19:15")中，只需要存下每个字符出现的个数，然后直接在字符串中遍历；

2）流：字符流没有存下来，无法进行遍历，因此在本题中，只能在数据容器哈希表中遍历，而且哈希表中存放的是对应字符的位置，而不是个数。

2.记得会用构造函数来初始化参数；

3.Integer.MAX_VALUE=2^31-1，是32位操作系统（4字节）中最大的符号型整型常量。

4.分清楚：字符与ASCII码的转化，以及 字符形式的数字转和整型数字间的转化

    
    
    	public static void main(String[] args) {
    		//字符转化为ASCII码
    		char ch_a = 'a';
    		int code_a = (int)ch_a; // =ASCII码97
    		
    		//ASCII码转化为字符
    		char copyCh_a = (char) code_a;  // =ASCII码97对应的字符'a'
    		
    		//字符形式数字转化为整型
    		char c1 = '2';
    		int n1 = c1-'0';  //=2, 由'2'和'1'的ASCII码相减得到
    		
    		//数字转化为字符形式
    		char copyC1 = (char)(n1+'0');  //='2' ,由'0'的ASCII码加2得到'2'的ASCII码
    		System.out.println(5);
    	}	
    

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)