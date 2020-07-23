# 【Java】 剑指offer(19) 正则表达式匹配  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现一个函数用来匹配包含'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"及"ab*a"均不匹配。

## 思路

使用函数matchCore(char[] str, int indexOfStr, char[] pattern, int indexOfPattern)
来实现每一步的比较（递归）。

（1）当模式中第二个字符不为“*”时：若当前字符相等，则字符串和模式都后移一个字符，继续调用函数进行比较；若不相等，则返回false。

（2）当模式中第二个字符为“*”时：若当前字符不相等，则模式后移两个字符，继续比较；若当前字符相等，则有三种情况：

1）字符串字符位置不变，模式后移两个字符，继续比较； //x*被忽略

2）字符串后移一个字符，模式后移两个字符，继续比较；

3）字符串后移一个字符，模式字符位置不变，继续比较。

三种情况使用“||”进行并列比较。

**注意点**

时刻要注意数组是否越界！

**测试算例**

1.功能测试（模式中包含普通字符、“.”、“*”；匹配情况；不匹配情况）

2.特殊测试（null，空字符串）

## **完整Java代码**

（含测试代码)

    
    
    package _19;
    
    /**
     * 
     * @Description 面试题19：正则表达式匹配
     *
     * @author yongh
     * @date 2018年9月21日 上午8:12:06
     */
    
    // 题目：请实现一个函数用来匹配包含'.'和'*'的正则表达式。模式中的字符'.'
    // 表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题
    // 中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"
    // 和"ab*ac*a"匹配，但与"aa.a"及"ab*a"均不匹配。
    
    public class RegularExpressions {
    	public boolean match(char[] str, char[] pattern) {
    		if (str == null || pattern == null)
    			return false;
    		return matchCore(str, 0, pattern, 0);
    	}
    
    	private boolean matchCore(char[] str, int indexOfStr, char[] pattern, int indexOfPattern) {
    		if (indexOfStr == str.length && indexOfPattern == pattern.length)
    			return true;
    		if (indexOfStr < str.length && indexOfPattern == pattern.length)
    			return false;
    		if (indexOfPattern + 1 < pattern.length && pattern[indexOfPattern + 1] == '*') {
    			if ((indexOfStr < str.length && pattern[indexOfPattern] == '.')
    					|| (indexOfStr < str.length && pattern[indexOfPattern] == str[indexOfStr])) {
    				return matchCore(str, indexOfStr, pattern, indexOfPattern + 2)
    						|| matchCore(str, indexOfStr + 1, pattern, indexOfPattern)
    						|| matchCore(str, indexOfStr + 1, pattern, indexOfPattern + 2);
    			} else {
    				return matchCore(str, indexOfStr, pattern, indexOfPattern + 2);
    			}
    		}
    		if (indexOfStr < str.length && (pattern[indexOfPattern] == str[indexOfStr] || pattern[indexOfPattern] == '.'))
    			return matchCore(str, indexOfStr + 1, pattern, indexOfPattern + 1);
    		return false;
    	}
    
    	// ==========测试代码=========
    	void test(String testName, char[] str, char[] pattern, boolean expected) {
    		System.out.print(testName + ":");
    		if (match(str, pattern) == expected)
    			System.out.println("passed!");
    		else
    			System.out.println("failed!");
    	}
    
    	void test1() {
    		char[] str = {};
    		char[] pattern = { '.' };
    		test("test1", str, pattern, false);
    	}
    
    	void test2() {
    		char[] str = {};
    		char[] pattern = { '.', '*' };
    		test("test2", str, pattern, true);
    	}
    
    	void test3() {
    		char[] str = { 'a' };
    		char[] pattern = { '.', '*' };
    		test("test3", str, pattern, true);
    	}
    
    	void test4() {
    		char[] str = {};
    		char[] pattern = {};
    		test("test4", str, pattern, true);
    	}
    
    	void test5() {
    		char[] str = null;
    		char[] pattern = null;
    		test("test5", str, pattern, false);
    	}
    
    	void test6() {
    		char[] str = { 'a', 'b', 'b' };
    		char[] pattern = { 'a', 'b', 'b', '*', 'b' };
    		test("test6", str, pattern, true);
    	}
    
    	void test7() {
    		char[] str = { 'a' };
    		char[] pattern = { 'a', 'a', '*' };
    		test("test7", str, pattern, true);
    	}
    
    	public static void main(String[] args) {
    		RegularExpressions demo = new RegularExpressions();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    		demo.test7();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    test1:passed!
    test2:passed!
    test3:passed!
    test4:passed!
    test5:passed!
    test6:passed!
    test7:passed!

RegularExpressions

## **收获**

1.涉及到数组的情况下，一定要时刻注意数组越界问题！

2.对于每一步都是采用相同判断方法的题目，可以采用递归函数来实现

3.思维一定要全面，把握住关键矛盾，将每种情况考虑清楚。例如这道题，关键就在于第二个字符是否为“*”，确定关键问题后，分析清楚每一种情况即可

4.代码第29行的 indexOfStr  < str.length 一定要记得加，否则可能会出现重复执行第32行的情况。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)