# 【Java】 剑指offer(40) 最小的k个数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入n个整数，找出其中最小的k个数。例如输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

## 思路

**思路一：** 同[剑指offer(39)
数组中出现次数超过一半的数字](https://www.cnblogs.com/yongh/p/9938889.html)中使用partition()方法，基于数组的第k个数字调整，使得更小的k个数字都在数组左边即可。

**思路二：**
依次遍历n个整数，用一个容器存放最小的k个数字，每遇到比容器中最大的数字还小的数字时，将最大值替换为该数字。容器可以使用最大堆或者红黑树来实现。本文根据堆排序的原理来实现。

**测试算例** ****

1.功能测试（数组中存在/不存在重复数字）

2.边界值测试（k=1或者等于数组长度）

2.特殊测试（null、k <1、k大于数组长度）

## **Java代码**

    
    
    //题目：输入n个整数，找出其中最小的k个数。例如输入4、5、1、6、2、7、3、8
    //这8个数字，则最小的4个数字是1、2、3、4。
    
    public class KLeastNumbers {
      
        /*
         * 方法一：采用partition()
         */
        public ArrayList<Integer> GetLeastNumbers_Solution1(int [] input, int k) {
            ArrayList<Integer> leastNumbers = new ArrayList<Integer>();
            while(input==null || k<=0 || k>input.length)
                return leastNumbers;
            int start=0;
            int end=input.length-1;
            int index=partition(input,start,end);
            while(index!=k-1){
                if(index<k-1){
                    start=index+1;
                    index=partition(input,start,end);
                }else{
                    end=index-1;
                    index=partition(input,start,end);
                }
            }
            for(int i=0;i<k;i++){
                leastNumbers.add(input[i]);
            }
            return leastNumbers;
        }
         
        private int partition(int[] arr, int start,int end){
            int pivotKey=arr[start];
            while(start<end){
                while(start<end && arr[end]>=pivotKey)
                    end--;
                swap(arr,start,end);
                while(start<end && arr[start]<=pivotKey)
                    start++;
                swap(arr,start,end);
            }
            return start;
        }
         
        private void swap(int[] arr, int i,int j){
            int temp=arr[i];
            arr[i]=arr[j];
            arr[j]=temp;
        }
        
        /*
         * 方法二：基于堆的容器
         */
        public ArrayList<Integer> GetLeastNumbers_Solution2(int [] input, int k) {
            ArrayList<Integer> leastNumbers = new ArrayList<Integer>();
            while(input==null || k<=0 || k>input.length)
                return leastNumbers;
            int[] numbers=new int[k];  //用于放最小的k个数
            for(int i=0;i<k;i++)
                numbers[i]=input[i];//先放入前k个数
            for(int i=k/2-1;i>=0;i--){
                adjustHeap(numbers,i,k-1);//将数组构造成最大堆形式
            }
            for(int i=k;i<input.length;i++){
                if(input[i]<numbers[0]){ //存在更小的数字时
                    numbers[0]=input[i];
                    adjustHeap(numbers,0,k-1);//重新调整最大堆
                }
            }
            for(int n:numbers)
                leastNumbers.add(n);
            return leastNumbers;
        }
         
        //最大堆的调整方法，忘记时可以复习一下堆排序。
        private void adjustHeap(int[] arr,int start,int end){
            int temp=arr[start];
            int child=start*2+1;
            while(child<=end){
                if(child+1<=end && arr[child+1]>arr[child])
                    child++;
                if(arr[child]<temp)
                    break;
                arr[start]=arr[child];
                start=child;
                child=child*2+1;
            }
            arr[start]=temp;
        }
    }
    

大顶堆可以用PriorityQueue实现，所以方法二可利用API实现如下：

    
    
        public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
            ArrayList<Integer> list = new ArrayList<>();
            if(input==null || input.length<k || k<=0)
                return list;
            PriorityQueue<Integer> heap = new PriorityQueue<>(k,(i1, i2)->(i2-i1));
            for(int i=0; i<input.length; i++){
                if(heap.size()<k){
                    heap.offer(input[i]);
                }else if(heap.peek()>input[i]){
                    heap.poll();
                    heap.offer(input[i]);
                }
            }
            for(int i: heap)
                list.add(i);
            return list;
        }
    

## **收获**

1.k小于等于0的情况别忘记了

2.方法二，只需要在原始数组中进行读入操作，而所有的写操作和判断都是在容器中进行的，不用反复读取原始数组，思想非常好。

3.记得要弄清楚是否可以改变原始输入的数组。

4.partition函数：即是快速排序的基础，也可以用来查找n个数中第k大的数字。

5.当涉及到频繁查找和替换最大最小值时，二叉树是非常合适的数据结构，要能想到堆和二叉树。

6\. PriorityQueue重点：

* 大顶堆与小顶堆的构建: new Comporator()

* 如何插值: heap.offer(e)

* 如何获取堆顶的值: heap.peek(), heap.poll()

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)