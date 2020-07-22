# 【Java】 剑指offer(56-1) 数组中只出现一次的两个数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

## 思路

记住：两个相同的数字异或等于0.

如果数组中只有一个数字只出现一次，我们从头到尾异或每个数字，那么最终的结果刚好是那个只出现一次的数字。

而本题里数组中有两个数字只出现一次，如果能够将数组分为两部分，两部分中都只有一个数字只出现一次，那么就可以解决该问题了。

求解方法：

我们依旧从头到尾异或每个数字，那么最终的结果就是这两个只出现一次的数字的异或结果，由于两个数不同，因此这个结果数字中一定有一位为1，把结果中第一个1的位置记为第n位。因为是两个只出现一次的数字的异或结果，所以
这两个数字在第n位上的数字一定是1和0。

接下来我们根据数组中每个数字的第n位上的数字是否为1来进行分组，恰好能将数组分为两个都只有一个数字只出现一次的数组，对两个数组从头到尾异或，就可以得到这两个数了。

**测试算例** ****

1.功能测试（数组中有多对重复的数字；无重复的数字）

## **Java代码**

    
    
    //题目：一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序
    //找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。
    
    public class NumbersAppearOnce {
        public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
            if(array==null || array.length<2)
                return;
            int resultExclusiveOR=0;
            for(int i=0;i<array.length;i++)
                resultExclusiveOR^=array[i];
            
            int indexOf1=0;
            while(((resultExclusiveOR&1)==0) && (indexOf1<=4*8)){
            	resultExclusiveOR=resultExclusiveOR>>1;  //只有n>>1不完整，要n=n>>1
                indexOf1++;
            }
            
            num1[0]=0;
            num2[0]=0;
            for(int i=0;i<array.length;i++){
                if(((array[i]>>indexOf1)&1)==1)
                    num1[0]^=array[i];
                else
                    num2[0]^=array[i];
            }
        }
    }
    

## **收获**

1.当一个数字出现两次（或者 **偶数次** ）时，用异或^ 可以进行消除。 **一定要牢记 异或的这个功能！**

2.将一组数字分为两组，可以根据某位上是否为1来进行分组，即根据和1相与（ &1）的结果来进行分组。

3.判断某个数x的第n位（如第3位）上是否为1，

1）通过 x&00000100 的结果是否为0 来判断。（不能根据是否等于1来判断）

2）通过（x>>3)&1 是否为0 来判断

4.将某个数x右移m位，一定要写成 **x=x >>m；**而不能只写成 **x >>m；**这个语句

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)