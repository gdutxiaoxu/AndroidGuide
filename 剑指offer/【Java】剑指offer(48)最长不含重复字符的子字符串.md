# 【Java】 剑指offer(48) 最长不含重复字符的子字符串  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。假设字符串中只包含从'a'到'z'的字符。

## 思路

动态规划法：定义函数f(i)为：以第i个字符为 **结尾** 的不含重复字符的子字符串的最大长度。

（1）当第i个字符之前未出现过，则有：f(i)=f(i-1)+1

（2）当第i个字符之前出现过，记该字符与上次出现的位置距离为d

1）如果d<=f(i-1)，则有f(i)=d；

2）如果d>f(i-1)，则有f(i)=f(i-1)+1；

我们从第一个字符开始遍历，定义两个int变量preLength和curLength来分别代表f(i-1)和f(i)，再创建一个长度为26的pos数组来存放26个字母上次出现的位置，即可根据上述说明进行求解。

注意：每次最大长度和字母出现位置要记得更新。

**另一种思路：** 遍历每个字符，把当前字符看成子字符串的末尾结点，同时更新开头结点，详细代码见[Longest Substring Without
Repeating Characters](https://www.cnblogs.com/yongh/p/10071484.html)

**测试算例** ****

1.功能测试（一个或者多个字符，全部字符不同/相同）

2.特殊测试（null，空字符串）

## **Java代码**

    
    
    //题目：请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子
    //字符串的长度。假设字符串中只包含从'a'到'z'的字符。
    
    public class LongestSubstringWithoutDup {
    	public static int  maxLength(String str) {
    		if(str==null || str.length()<=0)
    			return 0;
    		int preLength=0;  //即f(i-1)
    		int curLength=0;  //即f(i)
    		int maxLength=0;
    		int[] pos= new int[26];  //用于存放字母上次出现的位置
    		for(int i=0;i<pos.length;i++)
    			pos[i]=-1;
    		for(int i=0;i<str.length();i++) {
    			int letterNumber = str.charAt(i)-'a';
    			if(pos[letterNumber]<0 || i-pos[letterNumber]>preLength) {
    				curLength=preLength+1;
    			}else {
    				curLength=i-pos[letterNumber];
    			}
    			pos[letterNumber]=i;
    			if(curLength>maxLength)
    				maxLength=curLength;			
    			preLength=curLength;
    		}
    		return maxLength;
    	}
    	
    	public static void main(String[] args) {
    		System.out.println(maxLength("arabcacfr")==4);
    		System.out.println(maxLength("a")==1);
    		System.out.println(maxLength("aaa")==1);
    		System.out.println(maxLength("abcdef")==6);
    		System.out.println(maxLength("")==0);
    		System.out.println(maxLength(null)==0);
    	}
    }
    

## **收获**

1.函数f(i)为：以第i个字符为 **结尾**
的不含重复字符的子字符串的最大长度。而不是以第i个字符作为开头。第i个字符作为结尾可以方便与下一个字符进行联系。

2.学会用长度为26的数组来存放26个字母所在的位置下标。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)