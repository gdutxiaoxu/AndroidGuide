# 【Java】 剑指offer(1) 找出数组中重复的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

## **题目**

在一个长度为n的数组里的所有数字都在0到n-1的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2,
3, 1, 0, 2, 5, 3}，那么对应的输出是重复的数字2或者3。

## **思路**

从哈希表的思路拓展，重排数组：把扫描的每个数字（如数字m）放到其对应下标（m下标）的位置上，若同一位置有重复，则说明该数字重复。

（在动手写代码前应该先想好测试用例）

**测试用例**

1.数组中带一个或多个重复数字

2.数组中不包含重复的数字

3.无效输入测试用例（空数组，数组数字越界等）

## **完整Java代码**

（含测试代码）

    
    
    /**
     * @Description 找出数组中重复的数字 
     * 
     * @author yongh
     * @date 2018年7月16日 上午10:24:05
     */
    
    /*
     * 题目：在一个长度为n的数组里的所有数字都在0到n-1的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，
     * 也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。例如，如果输入长度为7的数组{2, 3, 1, 0, 2, 5, 3}，
     * 那么对应的输出是重复的数字2或者3。
     */
    public class FindDuplication {
    
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
    			if (a < 0 || a > arr.length - 1) {
    				System.out.println("数字大小超出范围！");
    				return -1;
    			}
    		}
    		for (int i = 0; i < arr.length; i++) {
    			int temp;
    			while (arr[i] != i) {
    				if (arr[arr[i]] == arr[i])
    					return arr[i];
    				// 交换arr[arr[i]]和arr[i]
    				temp = arr[i];
    				arr[i] = arr[temp];
    				arr[temp] = temp;
    			}
    		}
    		System.out.println("数组中无重复数字！");
    		return -1;
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
    	 *数组无重复数字
    	 */
    	public void test2() {
    		System.out.print("test2：");
    		int[] a = { 0, 1, 2, 3 };
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	/**
    	 *数组数字越界
    	 */
    	public void test3() {
    		System.out.print("test3：");
    		int[] a = { 1, 2, 3, 4 };
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	/**
    	 *数组带重复数字
    	 */
    	public void test4() {
    		System.out.print("test4：");
    		int[] a = { 1, 2, 3, 2, 4 };
    		int dup = getDuplicate(a);
    		if (dup >= 0)
    			System.out.println("重复数字为：" + dup);
    	}
    
    	public static void main(String[] args) {
    		FindDuplication f = new FindDuplication();
    		f.test1();
    		f.test2();
    		f.test3();
    		f.test4();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/ExpandedBlockStart.gif)

    
    
    test1：数组输入无效！
    test2：数组中无重复数字！
    test3：数字大小超出范围！
    test4：重复数字为：2

FindDuplication

## 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

====================================================================

在牛客网中提交的代码如下（不含测试代码）：

    
    
    public class Solution {
        // Parameters:
        //    numbers:     an array of integers
        //    length:      the length of array numbers
        //    duplication: (Output) the duplicated number in the array number,length of duplication array is 1,so using duplication[0] = ? in implementation;
        //                  Here duplication like pointor in C/C++, duplication[0] equal *duplication in C/C++
        //    这里要特别注意~返回任意重复的一个，赋值duplication[0]
        // Return value:       true if the input is valid, and there are some duplications in the array number
        //                     otherwise false
        public boolean duplicate(int numbers[],int length,int [] duplication) {
            if(numbers==null||length<=0)
                return false;
            for(int a:numbers){
                if(a<0||a>=length)
                    return false;
            }
             
            int temp;
            for(int i=0;i<length;i++){
                while(numbers[i]!=i){
                    if(numbers[numbers[i]]==numbers[i]){
                        duplication[0]=numbers[i];
                        return true;
                    }
                    temp=numbers[i];
                    numbers[i]=numbers[temp];
                    numbers[temp]=temp;
                }
            }
            return false;
        }
    }
    

这里有一个收获：在Java的方法中，可以用duplication[0]代替C/C++中的指针*duplication，从而在返回boolean的同时，也可以获得需要的数字。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)