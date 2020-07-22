# 【Java】 剑指offer(39) 数组中出现次数超过一半的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1, 2, 3, 2, 2, 2, 5, 4,
2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。

## 思路

**思路一：** 数字次数超过一半，则说明：排序之后数组中间的数字一定就是所求的数字。

利用partition()函数获得某一随机数字，其余数字按大小排在该数字的左右。若该数字下标刚好为n/2，则该数字即为所求数字；若小于n/2，则在右边部分继续查找；反之，左边部分查找。

**思路二：** 数字次数超过一半，则说明：该数字出现的次数比其他数字之和还多

遍历数组过程中保存两个值：一个是数组中某一数字，另一个是次数。遍历到下一个数字时，若与保存数字相同，则次数加1，反之减1。若次数=0，则保存下一个数字，次数重新设置为1。由于要找的数字出现的次数比其他数字之和还多，那么要找的数字肯定是最后一次把次数设置为1的数字。

也可以这样理解（来源牛客网:https://www.nowcoder.com/questionTerminal/e8a1b01a2df14cb2b228b30ee6a92163cm问前程:https://www.nowcoder.com/profile/429784）：

采用阵地攻守的思想：  
第一个数字作为第一个士兵，守阵地；count = 1；  
遇到相同元素，count++;  
遇到不相同元素，即为敌人，同归于尽,count--；当遇到count为0的情况，又以新的i值作为守阵地的士兵，继续下去，到最后还留在阵地上的士兵，
**有可能是** 主元素。  
再加一次循环，记录这个士兵的个数看是否大于数组一般即可。

**测试算例** ****

1.功能测试（存在或者不存在超过数组长度一半的数字）

2.特殊测试（null、1个数字）

## **Java代码**

    
    
    //题目：数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例
    //如输入一个长度为9的数组{1, 2, 3, 2, 2, 2, 5, 4, 2}。由于数字2在数组中
    //出现了5次，超过数组长度的一半，因此输出2。
    
    public class MoreThanHalfNumber {
        boolean isInputInvalid = true;
        
       //方法一：partition方法
        public int MoreThanHalfNum_Solution(int [] array) {
            if(array==null ||array.length<=0)
                return 0;
            int low=0;
            int high=array.length-1;
            int index=partition(array,low,high);
            while(index!=array.length>>1){
                if(index<array.length>>1){
                    low=index+1;
                    index=partition(array,low,high);
                }else{
                    high=index-1;
                    index=partition(array,low,high);
                }
            }
            //判断次数是否超过一半
            int num=array[index];
            int times=0;
            for(int i=0;i<array.length;i++){
                if(array[i]==num){
                    times++;
                }
            }
            if(times*2>array.length){
                isInputInvalid=false;
                return num;
            }
            return 0;
        }
        
        private int partition(int[] array,int low ,int high){
            int pivotKey=array[low];
            while(low<high){
                while(low<high &&  array[high]>=pivotKey)
                    high--;
                int temp=array[low];
                array[low]=array[high];
                array[high]=temp;
                while(low<high && array[low]<=pivotKey)
                    low++;
                temp=array[low];
                array[low]=array[high];
                array[high]=temp;
            }
            return low;
        }
        
        //方法二
        public int MoreThanHalfNum_Solution2(int [] array) {
            if(array==null || array.length<=0)
                return 0;
            int num=array[0];
            int count=1;
            for(int i=1;i<array.length;i++){
                if(count==0) {
                    num=array[i];
                    count++;
                }
                else if(array[i]==num)
                    count++;
                else
                    count--;
            }
            if(count>0){
                int times=0;
                for(int i=0;i<array.length;i++){
                    if(array[i]==num){
                        times++;
                    }
                }
                if(times*2>array.length){
                    isInputInvalid=false;
                    return num;
                }
            }
            return 0; 
        }
    }
    

## **收获**

1.length/2 用 length >>1 来代替，具有更高的效率；

2.本题中，找到了所求数字，别忘记 **判断该数字的次数是否超过一半** 。

3.题目所要求的返回值为int，所以如果数组不满足要求时，无法通过返回值来告知是否出错，所以这道题设置了一个全局变量来进行判断。调用该方法时，需要记得对全局变量进行检查。

4.方法一中，采用了partition()函数，该函数会改变修改的数组，因此在面试的时候，需要和面试官讨论是否可以修改数组。

5.两种方法的时间复杂度均为O(n)。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)