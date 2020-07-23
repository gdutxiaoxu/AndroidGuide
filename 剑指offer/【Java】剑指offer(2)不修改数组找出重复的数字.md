# 【Java】 剑指offer(2) 不修改数组找出重复的数字  

> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

## **题目**

在一个长度为n+1的数组里的所有数字都在1到n的范围内，所以数组中至少有一个数字是重复的。请找出数组中任意一个重复的数字，但不能修改输入的数组。例如，如果输入长度为8的数组{2,
3, 5, 4, 3, 2, 6, 7}，那么对应的输出是重复的数字2或者3。

## **思路**

数组长度为n+1，而数字只从1到n，说明
必定有重复数字。可以由二分查找法拓展：把1~n的数字从中间数字m分成两部分，若前一半1~m的数字数目超过m个，说明重复数字在前一半区间，否则，在后半区间m+1~n。每次在区间中都一分为二，知道找到重复数字。

**更简单的思路：** 把该数组看作一个链表，下标代表当前结点，值代表next指针，具体参考[Find the Duplicate
Number](https://www.cnblogs.com/yongh/p/9981582.html)，时间复杂度仅为O(n)

**测试用例**

1.数组中带一个或多个重复数字

2. 数组中不包含重复的数字

3.无效输入测试用例（空数组，数组数字越界等）

## **完整Java代码**

（含测试代码）


​    
​    /**
​     * 
​     * @Description 不修改数组找出重复的数字
​     *
​     * @author yongh
​     * @date 2018年7月16日 上午11:47:44
​     */
​    
    /*
     * 题目：在一个长度为n+1的数组里的所有数字都在1到n的范围内，所以数组中至
     * 少有一个数字是重复的。请找出数组中任意一个重复的数字，但不能修改输入的
     * 数组。例如，如果输入长度为8的数组{2, 3, 5, 4, 3, 2, 6, 7}，那么对应的
     * 输出是重复的数字2或者3。	
     */
    public class FindDuplication2 {
    
    	/**
    	 * 找到数组中一个重复的数字
    	 * 返回-1代表无重复数字或者输入无效
    	 */
    	public int getDuplicate(int[] arr) {
    		if (arr == null || arr.length <= 0) {
    			System.out.println("数组输入无效！");
    			return -1;
    		}
    		for (int a : arr) {
    			if (a < 1 || a > arr.length - 1) {
    				System.out.println("数字大小超出范围！");
    				return -1;
    			}
    		}
    		int low = 1;
    		int high = arr.length - 1; // high即为题目的n
    		int mid, count;
    		while (low <= high) {
    			mid = ((high - low) >> 2) + low;
    			count = countRange(arr, low, mid);
    			if (low == high) {
    				if (count > 1)
    					return low;
    				else
    					break; // 必有重复，应该不会出现这种情况吧？
    			}
    			if (count > mid - low + 1) {
    				high = mid;
    			} else {
    				low = mid + 1;
    			}
    		}
    		return -1;
    	}
    
    	/**
    	 * 返回在[low,high]范围中数字的个数 
    	 */
    	public int countRange(int[] arr, int low, int high) {
    		if (arr == null)
    			return 0;
    
    		int count = 0;
    		for (int a : arr) {
    			if (a >= low && a <= high)
    				count++;
    		}
    		return count;
    	}
    
    	// ==================================测试代码==================================
    	/**
    	 *数组为null
    	 */
    	public void test1() {
    		System.out.print("test1：");
    		int[] a = null;
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	/**
    	 *数组数字越界
    	 */
    	public void test2() {
    		System.out.print("test2：");
    		int[] a = { 1, 2, 3, 4 };
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	/**
    	 *数组带重复数字
    	 */
    	public void test3() {
    		System.out.print("test3：");
    		int[] a = { 1, 2, 3, 2, 4 };
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	public static void main(String[] args) {
    		FindDuplication2 f2 = new FindDuplication2();
    		f2.test1();
    		f2.test2();
    		f2.test3();
    	}
    }


![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)
![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)


​    
​    test1：数组输入无效！
​    test2：数字大小超出范围！
​    test3：重复数字为：2

FindDuplication2

## 复杂度

时间复杂度说明：函数countRange()将被调用O(logn)次，每次需要O(n)的时间。

时间复杂度：O(nlogn) （while循环为O(logn)，coutRange()函数为O(n)）

空间复杂度：O(1)

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)