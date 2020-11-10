# 【Java】 剑指offer(13) 剪绳子  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

[leetcode](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/solution/dong-tai-gui-hua-shu-xue-by-sophia_fez/)

## 题目

给你一根长度为n绳子，请把绳子剪成m段（m、n都是整数，n＞1并且m＞1）。每段的绳子的长度记为k[0]、k[1]、……、k[m]。k[0]*k[1]*…*k[m]可能的最大乘积是多少？例如当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到最大的乘积18。

## 思路

本题采用动态规划或者贪婪算法可以实现。一开始没有思路时，可以从简单的情况开始想，试着算以下比较短的绳子是如何剪的。

当n=1时，最大乘积只能为0；

当n=2时，最大乘积只能为1；

当n=3时，最大乘积只能为2；

当n=4时，可以分为如下几种情况:1*1*1*1，1*2*1，1*3，2*2，最大乘积为4；

往下推时，发现n≥4时，可以把问题变成几个小问题，即：如果把长度n绳子的最大乘积记为f(n)，则有：f(n)=max(f(i)*f(n-1))，0
<i<n。所以思路就很容易出来了：从下往上推，先算小的问题，再算大的问题，大的问题通过寻找小问题的最优组合得到。

其实这就是动态规划法，以下是动态规划法的几个特点：

1.求一个问题的最优解

2.整体问题的最优解依赖各子问题的最优解

3.小问题之间还有相互重叠的更小的子问题

4.为了避免小问题的重复求解，采用从上往下分析和从下往上求解的方法求解问题

贪婪算法依赖于数学证明，当绳子大于5时，尽量多地剪出长度为3的绳子是最优解。

**测试用例**

1.功能测试（长度大于5）

2.边界值测试（长度1，2，3，4）

## **完整Java代码**

（含测试代码，测试代码参考CuttingRope.cpp:https://github.com/zhedahht/CodingInterviewChinese2/blob/master/14_CuttingRope/CuttingRope.cpp）

    
    
    /**
     * 
     * @Description 面试题14：剪绳子
     *
     * @author yongh
     * @date 2018年9月17日 上午9:37:41
     */
    
    // 题目：给你一根长度为n绳子，请把绳子剪成m段（m、n都是整数，n>1并且m≥1）。
    // 每段的绳子的长度记为k[0]、k[1]、……、k[m]。k[0]*k[1]*…*k[m]可能的最大乘
    // 积是多少？例如当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此
    // 时得到最大的乘积18。
    
    public class CuttingRope {
    	// ======动态规划======
    	public int maxProductAfterCutting_solution1(int length) {
    		if (length <= 1)
    			return 0;
    		if (length == 2)
    			return 1;
    		if (length == 3)
    			return 2;
    		int[] product = new int[length + 1]; // 用于存放最大乘积值
    		// 下面几个不是乘积，因为其本身长度比乘积大
    		product[0] = 0;
    		product[1] = 1;
    		product[2] = 2;
    		product[3] = 3;
    
    		// 开始从下到上计算长度为i绳子的最大乘积值product[i]
    		for (int i = 4; i <= length; i++) {
    			int max = 0;
    			// 算不同子长度的乘积，找出最大的乘积
    			for (int j = 1; j <= i / 2; j++) {
    				if (max < product[j] * product[i - j])
    					max = product[j] * product[i - j];
    			}
    			product[i] = max;
    		}
    		return product[length];
    	}
    
    	// =======贪婪算法========
    	public int maxProductAfterCutting_solution2(int length) {
    		if (length <= 1)
    			return 0;
    		if (length == 2)
    			return 1;
    		if (length == 3)
    			return 2;
    		int timesOf3 = length / 3;
    		int timesOf2 = 0;
    		if (length - timesOf3 * 3 == 1) {
    			timesOf3--;
    			// timesOf2=2;  //错误！
    		}
    		timesOf2 = (length - timesOf3 * 3) / 2;
    		return (int) (Math.pow(3, timesOf3) * Math.pow(2, timesOf2));
    	}
    
    	// =====测试代码======
    	void test(String testName, int length, int expected) {
    		if (testName != null)
    			System.out.println(testName + ":");
    		if (maxProductAfterCutting_solution1(length) == expected) {
    			System.out.print("    动态规划:" + "passed  ");
    		} else {
    			System.out.print("    动态规划:" + "failed  ");
    		}
    
    		if (maxProductAfterCutting_solution2(length) == expected) {
    			System.out.println("贪婪算法:" + "passed  ");
    		} else {
    			System.out.println("贪婪算法:" + "failed  ");
    		}
    	}
    
    	void test1() {
    		test("test1", 1, 0);
    	}
    
    	void test2() {
    		test("test2", 2, 1);
    	}
    
    	void test3() {
    		test("test3", 3, 2);
    	}
    
    	void test4() {
    		test("test4", 4, 4);
    	}
    
    	void test5() {
    		test("test5", 5, 6);
    	}
    
    	void test6() {
    		test("test6", 10, 36);
    	}
    
    	void test7() {
    		test("test7", 50, 86093442);
    	}
    
    	public static void main(String[] args) {
    		CuttingRope demo = new CuttingRope();
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

    
    
    test1:
        动态规划:passed  贪婪算法:passed  
    test2:
        动态规划:passed  贪婪算法:passed  
    test3:
        动态规划:passed  贪婪算法:passed  
    test4:
        动态规划:passed  贪婪算法:passed  
    test5:
        动态规划:passed  贪婪算法:passed  
    test6:
        动态规划:passed  贪婪算法:passed  
    test7:
        动态规划:passed  贪婪算法:passed  

CuttingRope

## **收获**

1.最优解问题，经常使用动态规划法，关键要刻画最优解的结构特征（本题的f(n)），从下往上计算最优解的值，没有思路时，从简单情况先算一下。

2.动态规划法中，子问题的最优解一般存放于一个数组中。

3.本题贪婪规划的代码中，timeOf2别忘记等于1的情况。

复习时补充：

1\. 动态规划法可以直接令 f(n)=max{f(n-2)*2,f(n-3)*3} 就可以了。

2\. 贪婪算法，第51-58行可改为

    
    
    		int timesOf3=n/3;
    		if(n%3==0)
    			return (int)Math.pow(3, timesOf3);
    		if(n%3==1)
    			return (int)Math.pow(3, timesOf3-1)*4;  //是乘以4，不是2
    		return (int)Math.pow(3, timesOf3)*2;
    

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)
