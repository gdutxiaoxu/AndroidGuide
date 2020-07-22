# 【Java】 剑指offer(53-1) 数字在排序数组中出现的次数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

**正文**

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

统计一个数字在排序数组中出现的次数。例如输入排序数组{1, 2, 3, 3,3, 3, 4, 5}和数字3，由于3在这个数组中出现了4次，因此输出4。

## 思路

分析：对于例子来说，如果采用二分法找到某一个3后，再往前遍历和往后遍历到第一个和最后一个3，在长度为n的数组中有可能出现O(n)个3，因此这样的扫描方法时间复杂度为
**O(n)** ，效率与从头到尾扫描一样，速度太慢。

这题关键是找到第一个和最后一个3，因此我们尝试改进二分法：中间数字比3大或者小的情况与之前类似，关键是中间数字等于3的情况，这时可以分类讨论如下：

1）如果中间数字的前一个数字也等于3，说明第一个3在前面，继续在前半段查找第一个3；

2）如果中间数字的前一个数字不等于3，说明该位置是第一个3；

3）如果中间数字的后一个数字也等于3，说明最后一个3在后面，继续在后半段查找最后一个3；

2）如果中间数字的后一个数字不等于3，说明该位置是最后一个3；

附加：牛客网上还有一种算法：如果找数字k的次数，由于数组是整数，可以直接找k-0.5和k+0.5应该在数组中哪个位置，这种方法就不用讨论这么多情况了。（不过double类型的大小比较不知道是否会增加太多时间消耗）。

**测试算例** ****

1.功能测试（数字出现次数为0、1、2等）

2.边界值测试（数组只有一个数字，查找数字为第一个或者最后一个）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：统计一个数字在排序数组中出现的次数。例如输入排序数组{1, 2, 3, 3,
    //3, 3, 4, 5}和数字3，由于3在这个数组中出现了4次，因此输出4。
    
    public class NumberOfK {
        public int GetNumberOfK(int [] array , int k) {
            if(array==null || array.length<=0)
                return 0;
             int firstK = getFirstK(array,0,array.length-1,k);
             if(firstK == -1)
                 return 0;
             int lastK = getLastK(array,firstK,array.length-1,k);
             return lastK-firstK+1;
         }
          
         private int getFirstK(int[] arr, int start, int end,int k){
             if(start>end)
                 return -1;
             int mid = (start+end)>>1;
             if(arr[mid]==k){
                 if( mid == 0 ||arr[mid-1]!=k )
                     return mid;
                 else
                     end = mid-1;
             }else if(arr[mid]<k){
                 start = mid+1;
             }else{
                 end = mid-1;
             }
             return getFirstK(arr,start,end,k);
         }
          
         private int getLastK(int[] arr, int start, int end,int k){
             if(start>end)
                 return -1;
             int mid = (start+end)>>1;
             if(arr[mid]==k){
                 if(mid==arr.length-1 || arr[mid+1]!=k )
                     return mid;
                 else
                     start = mid+1;
             }else if(arr[mid]<k){
                 start = mid+1;
             }else{
                 end = mid-1;
             }
             return getLastK(arr,start,end,k);
         }
    }
    

解法二：寻找k+0.5和k-0.5的方法：

    
    
        public int GetNumberOfK(int [] arr , int k) {
           if(arr==null || arr.length<=0)
               return 0;
            int first = getLoc(arr, k , k-0.5);
            int last = getLoc(arr,k,k+0.5);
            return last-first;
        }
        
        private int getLoc(int[]arr, int k, double m){ //同样是二分查找
            int start=0,end=arr.length-1;
            while(start<=end){
                int mid=(start+end)>>1;
                if(arr[mid]>m){
                    end=mid-1;
                }else{
                    start=mid+1;
                }
            }
            return start;
        }
    

## **收获**

1.53-3:https://www.cnblogs.com/yongh/p/9958138.html#_label3

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)