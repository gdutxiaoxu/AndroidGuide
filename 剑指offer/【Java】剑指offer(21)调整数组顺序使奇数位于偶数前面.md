# 【Java】 剑指offer(21) 调整数组顺序使奇数位于偶数前面  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

## 思路

对于任意一个整数数组，设置一个指针，从前往后走，如果遇到奇数则指针后移，遇到偶数时，希望把该偶数放在数组后面；因此，再设置一个指针，从后往前走，遇到偶数时指针前移，遇到奇数时，则恰好可以与前面的指针所指的偶数进行调换。

**测试算例** ****

1.功能测试（数组中奇偶数交替出现；数组中先奇数后偶数；数组中先偶数后奇数）

2.特殊测试（null，空数组，一个数据的数组）

## **完整Java代码**

（含测试代码)

    
    
    package _21;
    
    import java.util.Arrays;
    
    /**
     * 
     * @Description 调整数组顺序使奇数位于偶数前面 
     *
     * @author yongh
     * @date 2018年10月11日 上午10:12:01
     */
    
    //题目：输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有
    //奇数位于数组的前半部分，所有偶数位于数组的后半部分。
    
    public class ReorderArray {
    	
        public void reOrderArray(int [] array) {
            if(array==null || array.length==0)
                return;
            int length = array.length;
            int low=0;
            int high=length-1;
            int temp;
            while(low<high){
            	//向后移动low指针，直到它指向偶数
                while(low<length && (array[low]&1)!=0)
                    low++;
                //向前移动high指针，直到它指向奇数
                while(high>=0 && (array[high]&1)==0)
                    high--;
                if(low<high){               
                    temp=array[low];
                    array[low]=array[high];
                    array[high]=temp;
                }
            }
        }
        
        //===============测试代码===================
        void test1() {
        	int[] array = null;
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test2() {
        	int[] array = {};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test3() {
        	int[] array = {-2,4,-6,1,-3,5};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test4() {
        	int[] array = {-1,3,-5,2,-4,6};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test5() {
        	int[] array = {-1,2,-3,4,-5,6};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test6() {
        	int[] array = {2,2,1,3,4,1};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
        void test7() {
        	int[] array = {1};
        	System.out.println("原始数组："+Arrays.toString(array));
        	reOrderArray(array);
        	System.out.println("调整结果："+Arrays.toString(array));
        	System.out.println();
        }
        
    	public static void main(String[] args) {
    		ReorderArray demo = new ReorderArray();
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

    
    
    test1 passed!
    test2 passed!
    test3 passed!
    test4 passed!
    test5 passed!
    test6 passed!

ReorderArray

## 附加要求

如果题目附加要求：保证调整后的数组中，奇数和奇数之间，偶数和偶数之间的相对位置不变。

此时用上面的方法就没法实现该功能，可以采用类似于“直接插入排序”的方法：从头开始遍历，遇到奇数时，将该奇数插入到该奇数前面的偶数之前。（如：从头开始遍历246183，遇到奇数1时，将1插入到246之前，变为：124683；该插入的实质是：奇数前面的所有偶数往后移一位，空出的位置放入该奇数），具体实现方法见下面的代码：

    
    
        /*
         * 附加要求：保证调整后的数组中，奇数和奇数之间，偶数和偶数之间的相对位置不变。
         * 采用类似直接插入排序算法
         */
        public void reOrderArray2(int [] array) {
        	if(array==null || array.length==0)
                return;
        	int length = array.length;
        	int temp,j;
        	for(int i=1;i<length;i++) {
        		if((array[i]&1)!=0) {
        			j=i;
        			temp=array[j];
        			while((j>0)&&(array[j-1]&1)==0) {
        				array[j]=array[j-1];
        				j--;
        			}
        			array[j]=temp;
        		}
        	}
        }
    

## **收获**

学会灵活应用指针。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)