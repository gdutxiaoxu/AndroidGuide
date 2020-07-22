# 【Java】 剑指offer(10) 旋转数组的最小数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如数组{3, 4, 5, 1,
2}为{1, 2, 3, 4, 5}的一个旋转，该数组的最小值为1。

## 思路

数组在一定程度上是排序的，很容易分析出：可以采用二分法来寻找最小数字。

但是这里面有一些陷阱：

1.递增排序数组的本身是自己的旋转，则最小数字是第一个数字

2.中间数字与首尾数字大小相等，如{1,0,1,1,1,1}和{1,1,1,1,0,1}，无法采用二分法，只能顺序查找。

**测试用例**

1.功能测试（正常旋转数组，中间有或者无重复数字）

2.边界值测试（升序数组，1个数字的数组）

3.特殊输入测试（null，空数组）

## **完整Java代码**

（含测试代码）

    
    
    /**
     * 
     * @Description 旋转数组的最小数字
     *
     * @author yongh
     * @date 2018年9月14日 下午8:30:29
     */
    
    // 题目：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
    // 输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如数组
    // {3, 4, 5, 1, 2}为{1, 2, 3, 4, 5}的一个旋转，该数组的最小值为1。
    
    public class MinNumberInRotatedArray {
    	public int minNumberInRotateArray(int[] array) {
    		if (array == null || array.length <= 0) // 空数组或null时返回0
    			return 0;
    		int low = 0;
    		int high = array.length - 1;
    		int mid = (low + high) / 2;
    		//升序数组
    		if (array[low] < array[high])
    			return array[low];
    		//中间数字与首尾数字相等
    		if (array[mid] == array[high] && array[mid] == array[low]) {
    			for (int i = 1; i <= high; i++) {
    				if (array[i] < array[i - 1])
    					return array[i];
    			}
    			return array[low];
    		}
    		//正常情况
    		while (low < high) {
    			if (high - low == 1)
    				break;
    			mid = (low + high) / 2;
    			if (array[mid] <= array[high])
    				high = mid;
    			if (array[mid] > array[high])
    				low = mid;
    		}
    		return array[high]; // 别错写成了return high; !!
    	}
    
    	// =======测试代码======
    	public void test1() {
    		int[] array = null;
    		System.out.println("test1:" + minNumberInRotateArray(array));
    	}
    
    	public void test2() {
    		int[] array = {};
    		System.out.println("test2:" + minNumberInRotateArray(array));
    	}
    
    	public void test3() {
    		int[] array = { 1 };
    		System.out.println("test3:" + minNumberInRotateArray(array));
    	}
    
    	public void test4() {
    		int[] array = { 1, 2, 3, 4, 5, 6 };
    		System.out.println("test4:" + minNumberInRotateArray(array));
    	}
    
    	public void test5() {
    		int[] array = { 2, 2, 2, 2, 1, 2 };
    		System.out.println("test5:" + minNumberInRotateArray(array));
    	}
    
    	public void test6() {
    		int[] array = { 2, 1, 2, 2, 2, 2 };
    		System.out.println("test6:" + minNumberInRotateArray(array));
    	}
    
    	public void test7() {
    		int[] array = { 6, 6, 8, 9, 10, 1, 2, 2, 3, 3, 4, 5, 6 };
    		System.out.println("test7:" + minNumberInRotateArray(array));
    	}
    
    	public static void main(String[] args) {
    		MinNumberInRotatedArray demo = new MinNumberInRotatedArray();
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

    
    
    test1:0
    test2:0
    test3:1
    test4:1
    test5:1
    test6:1
    test7:1

MinNumberInRotatedArray

**代码学习**

下面的代码是牛客网中FINACK:https://www.nowcoder.com/profile/519819写的代码，非常简略。在保证可读性的情况下，希望自己也能早日写出简洁高效的代码。

    
    
    public class Solution {
        public int minNumberInRotateArray(int [] array) {
            int low = 0 ; int high = array.length - 1;   
            while(low < high){
                int mid = low + (high - low) / 2;        
                if(array[mid] > array[high]){
                    low = mid + 1;
                }else if(array[mid] == array[high]){
                    high = high - 1;
                }else{
                    high = mid;
                }   
            }
            return array[low];
        }
    }
    

注意这段代码的一些细节：

1.使用low=mid+1，而不是low=mid，最终会使得low=high（即最小值位置）而跳出循环；

2.使用high=mid，而不是high=mid-1，因为有可能mid就是最小值点，不能减1；

3.升序数组的情况可以直接在循环中一起搞定，不用单独列出来判断（自己的代码还可以改进）

小瑕疵：

1.该程序在array[mid] = array[high]时直接顺序查找。但其实这还有可能可以用二分法的，除非还满足array[mid] =
array[low]，才只能使用顺序查找。所以可以先排除掉必须顺序查找的情况（类似自己上面的程序，提前判断掉），之后就可以直接删除else
if(array[mid] == array[high]){high = high - 1;这两行了。

2.缺少null的判断。

## **收获**

1.对于一些涉及数组的方法（如二分法等），可以用low和high，mid等来定义下标，但是，输出时如果要求输出数据值array[low]，不要错写成下标low了。

2.思维一定要考虑全面，特别是接触到一个新的概念时，要注意到一些特例，如递增排序数组的本身是自己的旋转、相同数字数组等。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)