# 【Java】 剑指offer(20) 表示数值的字符串  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串“+100”、“5e2”、“-123”、“3.1416”及“-1E-16”都表示数值，但“12e”、“1a3.14”、“1.2.3”、“+-5”及“12e+5.4”都不是。

## 思路

刚开始的思路是从头到尾遍历，对遇到的不同情况进行分析，但很容易出错。因此采用《剑指OFFER》一书的方法：将数字的形式总结为：(A.B E/e A)
,按顺序进行判断（A代表带符号整数，B代表不带符号整数）。

另一种思路：借助几个flag从头到尾遍历，具体代码见：[【LeetCode】65. Valid
Number](https://www.cnblogs.com/yongh/p/10067651.html "发布于2018-12-04 22:02")

**测试算例** ****

1.功能测试（正负数；含整数与不含整数部分；含与不含小数部分；含与不含指数部分；不匹配情况）

2.特殊测试（null，空字符串）

## **完整Java代码**

（含测试代码)

    
    
    /**
     * 
     * @Description 面试题20：表示数值的字符串
     *
     * @author yongh
     * @date 2018年9月22日 上午11:15:13
     */
    
    // 题目：请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，
    // 字符串“+100”、“5e2”、“-123”、“3.1416”及“-1E-16”都表示数值，但“12e”、
    // “1a3.14”、“1.2.3”、“+-5”及“12e+5.4”都不是
    
    public class NumericStrings {
    	/*
    	 *  数字的基本格式为：(A.B E/e A) ,按顺序进行判断
    	 *  //A代表带符号整数，B代表不带符号整数
    	 *  小心：时刻要注意数组越界问题！
    	 */
    
    	public boolean isNumeric(char[] str) {
    		if (str == null || str.length == 0)
    			return false;
    		int[] index = new int[1];
    		index[0] = 0; // 用于记录当前字符位置
    		// 先判断A
    		boolean isNumeric; //用于记录是否满足条件
    		isNumeric = isInteger(str, index);
    		// 判断B
    		if (index[0] < str.length && (str[index[0]] == '.')) {
    			index[0]++;
    			isNumeric = isUnsignedInteger(str, index) || isNumeric; // .B和A.和A.B形式均可以
    		}
    		// 判断e后面的A
    		if (index[0] < str.length && (str[index[0]] == 'e' || str[index[0]] == 'E')) {
    			index[0]++;
    			isNumeric = isInteger(str, index) && isNumeric;
    		}
    		if (isNumeric && index[0] == str.length)
    			return true;
    		else
    			return false;
    	}
    
    	private boolean isInteger(char[] str, int[] index) { // 用int[]才能传值，int的话需要定义index为全局变量
    		if (index[0] < str.length && (str[index[0]] == '+' || str[index[0]] == '-'))
    			index[0]++;
    		return isUnsignedInteger(str, index);
    	}
    
    	private boolean isUnsignedInteger(char[] str, int[] index) {
    		int start = index[0];
    		while (index[0] < str.length && (str[index[0]] - '0' <= 9 && str[index[0]] - '0' >= 0))
    			index[0]++;
    		if (index[0] > start)
    			return true;
    		else
    			return false;
    	}
    
    	// =======测试代码=========
    	void test(String testName, char[] str, boolean expected) {
    		System.out.print(testName + "：");
    		if (isNumeric(str) == expected)
    			System.out.println(" passed!");
    		else
    			System.out.println(" failed!");
    	}
    
    	void test1() {
    		char[] str = null;
    		test("test1", str, false);
    	}
    
    	void test2() {
    		char[] str = {};
    		test("test2", str, false);
    	}
    
    	void test3() {
    		String string ="e3";
    		char[] str=string.toCharArray();
    		test("test3", str, false);
    	}
    
    	void test4() {
    		String string ="3e1.2";
    		char[] str=string.toCharArray();
    		test("test4", str, false);
    	}
    	
    	void test5() {
    		String string ="e3";
    		char[] str=string.toCharArray();
    		test("test5", str, false);
    	}
    	
    	void test6() {
    		String string ="1.2e3";
    		char[] str=string.toCharArray();
    		test("test6", str, true);
    	}
    	
    	void test7() {
    		String string ="-.2e3";
    		char[] str=string.toCharArray();
    		test("test7", str, true);
    	}
    	
    	void test8() {
    		String string ="-.2e-3";
    		char[] str=string.toCharArray();
    		test("test8", str, true);
    	}
    	
    	void test9() {
    		String string ="1.e-3";
    		char[] str=string.toCharArray();
    		test("test9", str, true);
    	}
    	
    	void test10() {
    		String string ="1.";
    		char[] str=string.toCharArray();
    		test("test10", str, true);
    	}
    	
    	void test11() {
    		String string =".2";
    		char[] str=string.toCharArray();
    		test("test11", str, true);
    	}
    
    	void test12() {
    		String string ="12e3";
    		char[] str=string.toCharArray();
    		test("test12", str, true);
    	}
    	
    	public static void main(String[] args) {
    		NumericStrings demo = new NumericStrings();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    		demo.test7();
    		demo.test8();
    		demo.test9();
    		demo.test10();
    		demo.test11();
    		demo.test12();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    test1： passed!
    test2： passed!
    test3： passed!
    test4： passed!
    test5： passed!
    test6： passed!
    test7： passed!
    test8： passed!
    test9： passed!
    test10： passed!
    test11： passed!
    test12： passed!

NumericStrings

## **收获**

****
对字符串进行依次判断时，定义一个Boolean变量，每判断一部分进行更新，最终该变量即为判断结果，不需要进行循环判断。（即本例中的isNumeric变量）

代码38行，别忘记了最后对index是否到达结尾进行判断。

**注意：** 第31行```isNumeric = isUnsignedInteger(str, index) || isNumeric;
`的顺序不能反了，不能写成isNumeric = isNumeric || isUnsignedInteger(str, index) ;
否则当isNumeric为True时，不会判断后半部分，index就不会走向'e'，从而导致错误。`  
`

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)