# 【Java】 剑指offer(16) 打印1到最大的n位数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

[leetcode](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/solution/javajian-zhi-offeryuan-ti-jie-fa-by-toheng-2/)

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入数字n，按顺序打印出从1最大的n位十进制数。比如输入3，则打印出1、2、3一直到最大的3位数即999。

## 思路

**陷阱：** n过大时是大数问题，不能简单用int或者long数据输出，需要采用字符串或者数组表达大数。

**解决方法：** 通过字符数组char[]来进行输出数字。

**方法一：**

1）在字符串表达的数字上模拟加法；

2）把字符串表达的数字打印出来。

**方法二：**

1）采用递归将每一位都从0到9排列出来；

2）把字符串表达的数字打印出来。

·测试算例

功能测试（输入1，2，3……）

特殊输入测试（输入0，-1）

## **完整Java代码**

自己复习时写的方法（比第一次写的方法更清晰、简洁点）：

    
    
    	public void print1ToMaxOfNDights1s(int n) {
    		if(n<=0)
    			return;
    		char[] digit = new char[n];
    		for(int i=0;i<n;i++)
    			digit[i]='0';
    		for(int i=n-1;i>=0;i--) {
    			while(digit[i]!='9') {
    				int m=0;
    				digit[m]++;
    				while(m<n-1 && digit[m]>'9') {
    					digit[m]='0';
    					digit[m+1]++;
    					m++;
    				}
    				printdigits(digit);
    			}
    		}
    	}
    
    	private void printdigits(char[] digit) {
    		int m = digit.length-1;
    		while(digit[m]=='0')
    			m--;
    		for(int i=m;i>=0;i--)
    			System.out.print(digit[i]);
    		System.out.println();
    	}
    

（第一次写的代码，含测试)

    
    
    /**
     * 
     * @Description 面试题17：打印1到最大的n位数
     *
     * @author yongh
     * @date 2018年9月17日 下午9:07:53
     */
    
    // 题目：输入数字n，按顺序打印出从1最大的n位十进制数。比如输入3，则
    // 打印出1、2、3一直到最大的3位数即999。
    
    public class Print1ToMaxOfNDigits {
    	
    	//=========方法一============
    	/**
    	 * 采用模拟加一的方法
    	 */
    	public void print1ToMaxOfNDigits(int n) {
    		if (n <= 0)
    			return;
    		char[] number = new char[n];
    		// 不能用foreach方法对nuber[]赋值
    		// for (char c : number) {
    		// c = '0';
    		// }
    		for (int k = 0; k < number.length; k++)
    			number[k] = '0';
    		while (!increment(number)) {
    			printCharNumber(number);
    		}
    	}	
    	
    	/**
    	 * 对字符串进行加一操作，number达到最大值后返回true
    	 * 最低位加一；所有位如果超过10，则进位
    	 */
    	private boolean increment(char[] number) {
    		int nTakeOver = 0; // 代表进位
    		for (int i = number.length - 1; i >= 0; i--) {
    			int nSum = (number[i] - '0') + nTakeOver; // 当前位置数字
    			// number[i]-'0'是把char转化为int，nTakeOver代表进位
    			if (i == number.length - 1)
    				nSum++;
    			if (nSum >= 10) {
    				if (i == 0)
    					return true; // 超出范围了
    				nTakeOver = 1;
    				nSum -= 10;
    				number[i] = (char) (nSum + '0');
    			} else {
    				number[i] = (char) (nSum + '0');
    				break; // 高位不变，可以直接跳出循环了
    			}
    		}
    		return false;
    	}
    
    	/**
    	 * 打印字符数组形成的数字
    	 * 书中方法：利用布尔变量isBeginning0来从第一个非零字符打印
    	 */
    	private void printCharNumber(char[] number) {
    		boolean isBeginning0 = true;
    		for (int i = 0; i < number.length; i++) {
    			if (isBeginning0 && (number[i] - '0') != 0) {
    				isBeginning0 = false;
    			}
    			if (!isBeginning0) {
    				// System.out.print(number[i] - '0');
    				System.out.print(number[i]);
    			}
    		}
    		System.out.println();
    
    	}
    
    	/**
    	 * 打印字符数组形成的数字
    	 * 自己的方法：找出第一个非零字符位置，往后进行打印
    	 */
    	private void printCharNumber2(char[] number) {
    		int beginner = number.length; // 不写成number.length-1，以防写出0
    		for (int i = 0; i <= number.length - 1; i++) {
    			if ((number[i] - '0') != 0) {
    				beginner = i;
    				break;
    			}
    		}
    		for (int i = beginner; i <= number.length - 1; i++) {
    			System.out.print(number[i]);
    		}
    		if (beginner != number.length) // 数字为0时，换行符不输出
    			System.out.println();
    	}
    
    	
    	//=========方法二============
    	/**
    	 * 采用递归的方法
    	 */
    	public void print1ToMaxOfNDigits2(int n) {
    		if (n <= 0)
    			return;
    		char[] number = new char[n];
    		for (int k = 0; k < number.length; k++)
    			number[k] = '0';
    		for (int i = 0; i <= 9; i++) {
    			makeNumber(n, number, i, 0);
    		}
    	}
    
    	/**
    	 * 生成数字
    	 */
    	private void makeNumber(int n, char[] number, int nNumber, int index) {
    		if (index == number.length - 1) {
    			number[index] = (char) (nNumber + '0');
    			printCharNumber2(number); // 打印数字代码与第一个方法一样
    			return;
    		} else {
    			number[index] = (char) (nNumber + '0');
    			for (int i = 0; i <= 9; i++) {
    				makeNumber(n, number, i, index + 1);
    			}
    		}
    	}
    
    	// ========测试代码=============
    	void test(int nDigits) {
    		System.out.println("===test begin===");
    		System.out.println("method1:");
    		print1ToMaxOfNDigits(nDigits);
    		System.out.println("method2:");
    		print1ToMaxOfNDigits2(nDigits);
    		System.out.println("===test over===");
    	}
    
    	public static void main(String[] args) {
    		Print1ToMaxOfNDigits demo = new Print1ToMaxOfNDigits();
    		demo.test(-1);
    		demo.test(0);
    		demo.test(1);
    		demo.test(2);
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    ===test begin===
    method1:
    method2:
    ===test over===
    ===test begin===
    method1:
    method2:
    ===test over===
    ===test begin===
    method1:
    1
    2
    3
    4
    5
    6
    7
    8
    9
    method2:
    1
    2
    3
    4
    5
    6
    7
    8
    9
    ===test over===
    ===test begin===
    method1:
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77
    78
    79
    80
    81
    82
    83
    84
    85
    86
    87
    88
    89
    90
    91
    92
    93
    94
    95
    96
    97
    98
    99
    method2:
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77
    78
    79
    80
    81
    82
    83
    84
    85
    86
    87
    88
    89
    90
    91
    92
    93
    94
    95
    96
    97
    98
    99
    ===test over===

Print1ToMaxOfNDigits

## **收获**

1.任何时候都不能轻视题目，像这道题看起来简单，但其实涉及到大数问题，以后遇到数字相关的题目时要注意大数问题；

2.int类型和char类型转化，通过±‘0’来实现，int与char类型间的相互转换:https://www.cnblogs.com/yongh/p/9688259.html。

3.打印字符串表示的数组，从第一个非零数字打印。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)
