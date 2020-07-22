# 【Java】 剑指offer(14) 二进制中1的个数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现一个函数，输入一个整数，输出该数二进制表示中1的个数。例如把9表示成二进制是1001，有2位是1。因此如果输入9，该函数输出2。

## 思路

遇到与二进制有关的题目，应该想到位运算(与、或、异或、左移、右移)。

方法一：”与运算“有一个性质：通过与对应位上为1，其余位为0的数进行与运算，可以某一整数指定位上的值。这道题中，先把整数n与1做与运算，判断最低位是否为1；接着把1左移一位，与n做与运算，可以判断次低位是否为1……反复左移，即可对每一个位置都进行判断，从而可以获得1的个数。这种方法需要循环判断32次。

方法二（better）：如果一个整数不为0，把这个整数减1，那么原来处在整数最右边的1就会变为0，原来在1后面的所有的0都会变成1。其余所有位将不会受到影响。再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。因此，把一个整数减1，再和原来的整数做与运算，会把该整数最右边的1变成0。这种方法，整数中有几个1，就只需要循环判断几次。

**测试用例**

1.正数（包括边界值1、0x7FFFFFFF）

2.负数（包括边界值0x80000000、0xFFFFFFFF）

3.0

## **完整Java代码**

（含测试代码)

    
    
    /**
     * 
     * @Description 面试题15：二进制中1的个数
     *
     * @author yongh
     * @date 2018年9月17日 下午3:01:16
     */
    
    // 题目：请实现一个函数，输入一个整数，输出该数二进制表示中1的个数。例如
    // 把9表示成二进制是1001，有2位是1。因此如果输入9，该函数输出2。
    
    public class NumberOf1InBinary {
    	public int NumberOf1_Solution1(int n) {
    		int count = 0;
    		int flag = 1;
    		while (flag != 0) {
    			if ((flag & n) != 0)
    				count++;
    			flag = flag << 1;
    		}
    		return count;
    	}
    
    	public int NumberOf1_Solution2(int n) {
    		int count = 0;
    		while (n != 0) {
    			count++;
    			n = (n - 1) & n;
    		}
    		return count;
    	}
    
    	// =========测试代码=========
    
    	void test(String testName, int n, int expected) {
    		if (testName != null)
    			System.out.println(testName + ":");
    		if (NumberOf1_Solution1(n) == expected) {
    			System.out.print("    soluton1:" + "passed  ");
    		} else {
    			System.out.print("    solution1:" + "failed  ");
    		}
    
    		if (NumberOf1_Solution2(n) == expected) {
    			System.out.println("soluton2:" + "passed  ");
    		} else {
    			System.out.println("solution2:" + "failed  ");
    		}
    	}
    	
    	void test1() {
    		test("Test for 0", 0, 0);
    	}
    	
    	void test2() {
    		test("Test for 1", 1, 1);
    	}
    	
    	void test3() {
    		test("Test for 10", 10, 2);
    	}
    	
    	void test4() {
    		test("Test for 0x7FFFFFFF", 0x7FFFFFFF, 31);
    	}
    	
    	void test5() {
    		test("Test for 0xFFFFFFFF", 0xFFFFFFFF, 32);
    	}
    	
    	void test6() {
    		test("Test for 0x80000000", 0x80000000, 1);
    	}
    	
    	public static void main(String[] args) {
    		NumberOf1InBinary demo = new NumberOf1InBinary();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    		demo.test6();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    Test for 0:
        soluton1:passed  soluton2:passed  
    Test for 1:
        soluton1:passed  soluton2:passed  
    Test for 10:
        soluton1:passed  soluton2:passed  
    Test for 0x7FFFFFFF:
        soluton1:passed  soluton2:passed  
    Test for 0xFFFFFFFF:
        soluton1:passed  soluton2:passed  
    Test for 0x80000000:
        soluton1:passed  soluton2:passed  

NumberOf1InBinary

## **收获**

1.与二进制有关的题目要往位运算方面想，复习一下二进制位运算的几个用法:https://www.cnblogs.com/yongh/p/9971520.html

2.注意： **负数右移还是负数！** 即如果对n=0x8000
0000右移，最高位的1是不会变的。如果这道题目通过令n=n>>1来计算n中1的个数，该数最终会变成0xFFFF FFFF而陷入死循环！

3. **把一个整数减1，再和原来的整数做与运算，会把该整数最右边的1变成0。** 这种方法一定要牢牢记住，很多情况下都可能用到，例如：

_1）一句话判断一个整数是否为2的整数次方；_

_2）对两个整数m和n，计算需要改变m二进制表示中的几位才能得到n。_

4.与数字操作有关的题目，测试时注意边界值的问题。对于32位数字，其正数的边界值为1、0x7FFFFFFF，负数的边界值为0x80000000、0xFFFFFFFF。

5.几个细节问题

1）flag=flag <<1，而不是只写一句flag<<1;

2）flag&n！=0，而非flag&n==1； 也就不能写成count+=(flag&1)了

3）if语句中，不能写为if(flag&n!=0) ，而要写成 if((flag&n)!=0)，需要注意一下

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)