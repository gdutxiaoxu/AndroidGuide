# 【Java】 剑指offer(12) 机器人的运动范围  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

地上有一个m行n列的方格。一个机器人从坐标(0,
0)的格子开始移动，它每一次可以向左、右、上、下移动一格，但不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格(35,
37)，因为3+5+3+7=18。但它不能进入方格(35, 38)，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

## 思路

与[【Java】 剑指offer(11)
矩阵中的路径](https://www.cnblogs.com/yongh/p/9655745.html)类似，也采用回溯法，先判断机器人能否进入(i,j)，再判断周围4个格子。这题返回的是int值。

**测试用例**

1.功能测试（多行多列矩阵，k为正数）

2.边界值测试（矩阵只有一行或一列；k=0）

3.特殊输入测试（k为负数）

## **完整Java代码**

（含测试代码，测试代码引用于RobotMove.cpp:https://github.com/zhedahht/CodingInterviewChinese2/blob/master/13_RobotMove/RobotMove.cpp）

    
    
    /**
     * 
     * @Description 面试题13：机器人的运动范围
     *
     * @author yongh
     * @date 2018年9月17日 上午8:33:07
     */
    
    // 题目：地上有一个m行n列的方格。一个机器人从坐标(0, 0)的格子开始移动，它
    // 每一次可以向左、右、上、下移动一格，但不能进入行坐标和列坐标的数位之和
    // 大于k的格子。例如，当k为18时，机器人能够进入方格(35, 37)，因为3+5+3+7=18。
    // 但它不能进入方格(35, 38)，因为3+5+3+8=19。请问该机器人能够到达多少个格子？
    
    public class RobotMove {
    	public int movingCount(int threshold, int rows, int cols) {
    		if (rows <= 0 || cols <= 0 || threshold < 0)
    			return 0;
    
    		boolean[] isVisited = new boolean[rows * cols];
    		int count = movingCountCore(threshold, rows, cols, 0, 0, isVisited);// 用两种方法试一下
    		return count;
    	}
    
    	private int movingCountCore(int threshold, int rows, int cols, int row, int col, boolean[] isVisited) {
    		if (row < 0 || col < 0 || row >= rows || col >= cols || isVisited[row * cols + col]
    				|| cal(row) + cal(col) > threshold)
    			return 0;
    		isVisited[row * cols + col] = true;
    		return 1 + movingCountCore(threshold, rows, cols, row - 1, col, isVisited)
    				+ movingCountCore(threshold, rows, cols, row + 1, col, isVisited)
    				+ movingCountCore(threshold, rows, cols, row, col - 1, isVisited)
    				+ movingCountCore(threshold, rows, cols, row, col + 1, isVisited);
    	}
    
    	private int cal(int num) {
    		int sum = 0;
    		while (num > 0) {
    			sum += num % 10;
    			num /= 10;
    		}
    		return sum;
    	}
    
    	// ========测试代码=========
    	void test(String testName, int threshold, int rows, int cols, int expected) {
    		if (testName != null)
    			System.out.print(testName + ":");
    
    		if (movingCount(threshold, rows, cols) == expected)
    			System.out.println("Passed.");
    		else
    			System.out.println("Failed.");
    	}
    
    	// 方格多行多列
    	void test1() {
    		test("Test1", 5, 10, 10, 21);
    	}
    
    	// 方格多行多列
    	void test2() {
    		test("Test2", 15, 20, 20, 359);
    	}
    
    	// 方格只有一行，机器人只能到达部分方格
    	void test3() {
    		test("Test3", 10, 1, 100, 29);
    	}
    
    	// 方格只有一行，机器人能到达所有方格
    	void test4() {
    		test("Test4", 10, 1, 10, 10);
    	}
    
    	// 方格只有一列，机器人只能到达部分方格
    	void test5() {
    		test("Test5", 15, 100, 1, 79);
    	}
    
    	// 方格只有一列，机器人能到达所有方格
    	void test6() {
    		test("Test6", 15, 10, 1, 10);
    	}
    
    	// 方格只有一行一列
    	void test7() {
    		test("Test7", 15, 1, 1, 1);
    	}
    
    	// 方格只有一行一列
    	void test8() {
    		test("Test8", 0, 1, 1, 1);
    	}
    
    	// 机器人不能进入任意一个方格
    	void test9() {
    		test("Test9", -10, 10, 10, 0);
    	}
    
    	public static void main(String[] args) {
    		RobotMove demo = new RobotMove();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    		demo.test7();
    		demo.test8();
    		demo.test9();
    	}
    
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    Test1:Passed.
    Test2:Passed.
    Test3:Passed.
    Test4:Passed.
    Test5:Passed.
    Test6:Passed.
    Test7:Passed.
    Test8:Passed.
    Test9:Passed.

RobotMove

## **收获**

1.计算数位之和时，要注意数字不一定是十位数，可能是百位、千位甚至更多，所以cal()函数别写成计算十位数的方法了。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)