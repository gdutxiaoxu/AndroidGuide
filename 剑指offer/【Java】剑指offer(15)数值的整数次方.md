# 【Java】 剑指offer(15) 数值的整数次方  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

实现函数double Power(double base, int
exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

## 思路

这道题很容易实现，但需要注意以下陷阱：1）0的负数次方不存在；2）0的0次方没有数学意义；3）要考虑exponent为负数的情况。所以可以对exponent进行分类讨论，在对base是否为0进行讨论。

**测试用例**

指数和底数都分别设置为正负数和0.

## **完整Java代码**

（含测试代码)

    
    
    /**
     * 
     * @Description 面试题16：数值的整数次方
     *
     * @author yongh
     * @date 2018年9月17日 下午5:17:35
     */
    
    // 题目：实现函数double Power(double base, int exponent)，求base的exponent
    // 次方。不得使用库函数，同时不需要考虑大数问题。
    
    public class Power {
    
    	boolean IsInvalid = false;//用全局变量标记是否出错
    
    	public double power(double base, int exponent) {
    		IsInvalid = false;
    		double result; // double类型
    		if (exponent > 0) {
    			result = powerCore(base, exponent);
    		} else if (exponent < 0) {
    			if (base == 0) {
    				IsInvalid = true; //0的负数次方不存在
    				return 0;
    			}
    			result = 1 / powerCore(base, -exponent);
    		} else {
    			return 1; //这里0的0次方输出为1
    		}
    		return result;
    	}
    
    	private double powerCore(double base, int exponent) {		 
    		if (exponent == 1)
    			return base;
    		if (exponent == 0)
    			return 1;
    		double result = powerCore(base, exponent >> 1);
    		result *= result;
    		if ((exponent & 0x1) == 1)
    			result *= base;
    		return result;
    	}
    
    	// ========测试代码========
    	void test(String testName, double base, int exponent, double expected, boolean expectedFlag) {
    		if (testName != null)
    			System.out.print(testName + ":");
    		if (power(base, exponent) == expected && IsInvalid == expectedFlag) {
    			System.out.println("passed.");
    		} else {
    			System.out.println("failed.");
    		}
    	}
    
    	void test1() {
    		test("test1", 0, 6, 0, false);
    	}
    
    	void test2() {
    		test("test2", 0, -6, 0, true);
    	}
    
    	void test3() {
    		test("test3", 0, 0, 1, false);
    	}
    
    	void test4() {
    		test("test4", 2, 6, 64, false);
    	}
    
    	void test5() {
    		test("test5", 2, -3, 0.125, false);
    	}
    
    	void test6() {
    		test("test6", 5, 0, 1, false);
    	}
    
    	void test7() {
    		test("test7", -2, 6, 64, false);
    	}
    
    	public static void main(String[] args) {
    		Power demo = new Power();
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

    
    
    test1:passed.
    test2:passed.
    test3:passed.
    test4:passed.
    test5:passed.
    test6:passed.
    test7:passed.

Power

**非递归实现乘方：**

上面的powerCore()方法可改写如下：

    
    
    	/**
    	 * 非递归实现乘方
    	 */
    	private double powerCore2(double base, int exponent) {	
    		double result=1;
    		while(exponent!=0) {
    			if((exponent&0x1)==1)
    				result*=base;
    			exponent>>=1;  
    			base*=base; //指数右移一位，则底数翻倍
    			//举例：10^1101 = 10^0001*10^0100*10^1000
    			//即10^1+10^4+10^8
    		}
    		return result;
    	}
    

## **收获**

这道题虽然简单，但很有价值，收获如下：

1.double类型好像是不能直接用等号判断，因为存在误差（这里暂时用==好像没问题，不确定）

2.完全掌握快速做乘方的诀窍：涉及到求解某数的n次方问题时，可以采用递归来完成，即利用以下公式：

![](https://img2018.cnblogs.com/blog/1407330/201809/1407330-20180917192122945-1383901978.png)

3.使用右移运算符 >>代替除以2，有较高的效率： **exponent >> 1**

4.使用位与运算符代替求余运算符%判断奇偶数，有较高的效率： **if ((exponent & 0x1) == 1)**

（第三第四条以后在除以2时和判断奇偶时一定要下意识就能想到）

5.不要忽略底数为0而指数为负的情况。

6.非递归实现乘方，其本质是根据指数与2的倍数关系来对底数进行操作。

7. **if ((exponent & 0x1) == 1) **里面的小括号一定不能忘记！

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)