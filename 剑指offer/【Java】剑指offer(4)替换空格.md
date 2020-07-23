# 【Java】 剑指offer(4) 替换空格  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

_**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**_

## 题目

请实现一个函数，把字符串中的每个空格替换成"%20"。例如输入“We are happy.”，则输出“We%20are%20happy.”。

## 思路

首先要询问面试官是新建一个字符串还是在原有的字符串上修改，本题要求 在原有字符串上进行修改。

若从前往后依次替换，在每次遇到空格字符时，都需要移动后面O(n)个字符，对于含有O(n)个空格字符的字符串而言，总的时间效率为O(n2)。

转变思路：先计算出需要的总长度，然后从后往前进行复制和替换，，则每个字符只需要复制一次即可。时间效率为O(n)。

**测试用例**

1.字符串中无空格

2.字符串中含有空格（连续空格，空格在首尾等）

3.字符串为空字符串或者为null

## **完整Java代码**

1.根据牛客网的编程练习参考，方法的输入为StringBuffer（String无法改变长度，所以采用StringBuffer），输出为String。

主程序中，可以利用 StringBuffer sBuffer = new StringBuffer(str); 来获得字符串的StringBuffer。

2.代码中包含测试代码

    
    
    /**
     * 
     * @Description 替换空格 
     *
     * @author yongh
     * @date 2018年7月18日 上午11:25:52
     */
    
    // 题目：请实现一个函数，把字符串中的每个空格替换成"%20"。例如输入“We are happy.”，
    // 则输出“We%20are%20happy.”。
    
    public class ReplaceSpaces {
    
    	/**
    	 * 实现空格的替换
    	 */
    	public String replaceSpace(StringBuffer str) {
    		if (str == null) {
    			System.out.println("输入错误！");
    			return null;
    		}
    		int length = str.length();
    		int indexOfOriginal = length-1;
    		for (int i = 0; i < str.length(); i++) {
    			if (str.charAt(i) == ' ')
    				length += 2;
    		}
    		str.setLength(length);
    		int indexOfNew = length-1;
    		while (indexOfNew > indexOfOriginal) {
    			if (str.charAt(indexOfOriginal) != ' ') {
    				str.setCharAt(indexOfNew--, str.charAt(indexOfOriginal));
    			} else {
    				str.setCharAt(indexOfNew--, '0');
    				str.setCharAt(indexOfNew--, '2');
    				str.setCharAt(indexOfNew--, '%');
    			}
    			indexOfOriginal--;
    		}
    		return str.toString();
    	}
    	
        // ==================================测试代码==================================
    
    	/**
    	 * 输入为null
    	 */
    	public void test1() {
    		System.out.print("Test1：");
    		StringBuffer sBuffer = null;
    		String s = replaceSpace(sBuffer);
    		System.out.println(s);
    	}
    	
    	/**
    	 * 输入为空字符串
    	 */
    	public void test2() {
    		System.out.print("Test2：");
    		StringBuffer sBuffer = new StringBuffer("");
    		String s = replaceSpace(sBuffer);
    		System.out.println(s);
    	}
    	
    	/**
    	 * 输入字符串无空格
    	 */
    	public void test3() {
    		System.out.print("Test3：");
    		StringBuffer sBuffer = new StringBuffer("abc");
    		String s = replaceSpace(sBuffer);
    		System.out.println(s);
    	}
    	
    	/**
    	 * 输入字符串为首尾空格，中间连续空格
    	 */
    	public void test4() {
    		System.out.print("Test4：");
    		StringBuffer sBuffer = new StringBuffer(" a b  c  ");
    		String s = replaceSpace(sBuffer);
    		System.out.println(s);
    	}
    	
    	public static void main(String[] args) {
    		ReplaceSpaces rs = new ReplaceSpaces();
    		rs.test1();
    		rs.test2();
    		rs.test3();
    		rs.test4();
    	}
    }

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    Test1：输入错误！
    null
    Test2：
    Test3：abc
    Test4：%20a%20b%20%20c%20%20

ReplaceSpaces

**收获：** 如果在从前往后进行复制时，需要多次移动数据，则可以考虑从后往前复制，从而减小移动次数，提高效率。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)