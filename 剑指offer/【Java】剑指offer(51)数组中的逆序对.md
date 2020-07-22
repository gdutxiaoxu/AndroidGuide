# 【Java】 剑指offer(51)数组中的逆序对  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

在数组中的两个数字如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

## 思路

如果遍历数组，对每个数字都和后面的数字比较大小，时间复杂度为O(n^2)，效率太低。

利归并排序:https://www.cnblogs.com/yongh/p/9954732.html的思想，先将数组分解成为n个长度为1的子数组，然后进行两两合并同时排好顺序。

在对两个子区域合并排序时，记左边区域（下标为start~mid）的指针为i，右边区域（下标为mid+1~end）的指针为j，两个指针都指向该区域内最大的数字，排序时：

（1）如果i指向的数字大于j指向的数字，说明：逆序对有j-mid个，我们把i指向的数字放入临时创建的排序数组中，然后令i-1，指向该区域前一个数字，继续进行排序；

（2）如果i指向的数字小于等于j指向的数字，说明暂时不存在逆序对，将j指向的数字放入临时创建的排序数组中，然后令j-1，指向该区域前一个数字，继续进行排序；

（3）某一子区域数字都放入排序数组后，将另一个子区域剩下的数字放入排序数组中，完成排序；

（4）最后将排序好的数字按顺序赋值给原始数组的两个子区域，以便合并后的区域与别的区域合并。

![](https://img2018.cnblogs.com/blog/1407330/201811/1407330-20181114084308747-1926985388.png)

**测试算例** ****

1.功能测试（普通数组，递增数组，递减数组，含重复数字）

2.边界值测试（数组只有两个数字， **只有一个数字** ）

2.特殊测试（null）

## **Java代码、**

    
    
    //题目：在数组中的两个数字如果前面一个数字大于后面的数字，则这两个数字组
    //成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。
    
    public class InversePairs {
        public static int inversePairs(int [] array) {
            if(array==null || array.length<=0)
                return 0;
            int count=getCount(array,0,array.length-1);
            return count;
        }
        
        private static int getCount(int[] array,int start,int end){
            if(start>=end)
                return 0;
            int mid=(end+start)>>1;
            int left=getCount(array,start,mid);
            int right=getCount(array,mid+1,end);
            
            //合并
            int count=0;
            int i=mid; //左边区域的指针
            int j=end; //右边区域的指针
            int[] temp= new int[end-start+1];  //临时区域
            int k=end-start; //临时区域的指针
            while(i>=start && j>=mid+1){
                if(array[i]>array[j]){
                    count+=(j-mid);
                    temp[k--]=array[i--];
                }else{
                    temp[k--]=array[j--];
                }
            }
            while(i>=start)
                temp[k--]=array[i--];
            while(j>=mid+1)
                temp[k--]=array[j--];
            for(k=0;k<temp.length;k++)
                array[k+start]=temp[k];
            
            return count+left+right;
        }
    }
    

## **收获**

1.要对归并排序的实现非常熟练。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)