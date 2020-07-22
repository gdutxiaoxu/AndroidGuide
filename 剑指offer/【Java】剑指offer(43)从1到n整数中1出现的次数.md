# 【Java】 剑指offer(43) 从1到n整数中1出现的次数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个整数n，求从1到n这n个整数的十进制表示中1出现的次数。例如输入12，从1到12这些整数中包含1 的数字有1，10，11和12，1一共出现了5次。

## 思路

如果是从头到尾遍历(n次)，对每一个数字都计算其1的个数（lgn次），则时间复杂度为 **O(nlogn)** ，运算效率太低。因此必须总结规律，提高效率。

总结规律如下（思路比《剑指OFFER》一书简单）：

对于整数n，我们将这个整数分为三部分：当前位数字cur，更高位数字high，更低位数字low，如：对于n=21034，当位数是十位时，cur=3，high=210，low=4。

我们从个位到最高位 依次计算每个位置出现1的次数：

1）当前位的数字等于0时，例如n=21034，在百位上的数字cur=0，百位上是1的情况有：00100~00199，01100~01199，……，20100~20199。一共有21*100种情况，即high*100;

2）当前位的数字等于1时，例如n=21034，在千位上的数字cur=1，千位上是1的情况有：01000~01999，11000~11999，21000~21034。一共有2*1000+（34+1）种情况，即high*1000+(low+1)。

3）当前位的数字大于1时，例如n=21034，在十位上的数字cur=3，十位上是1的情况有：00010~00019，……，21010~21019。一共有（210+1）*10种情况，即(high+1)*10。

这个方法只需要遍历每个位数，对于整数n，其位数一共有lgn个，所以时间复杂度为 **O(logn)** 。

**测试算例** ****

1.功能测试（3，45，180等）

2.边界值测试（0，1等）

3.性能测试（输入较大的数字，如1000000等）

## **Java代码**

    
    
    //题目：输入一个整数n，求从1到n这n个整数的十进制表示中1出现的次数。例如
    //输入12，从1到12这些整数中包含1 的数字有1，10，11和12，1一共出现了5次。
    
    public class NumberOf1 {
        public int NumberOf1Between1AndN_Solution(int n) {
            int count=0;
            for(int i=1;i<=n;i*=10){  //i代表位数
                int high=n/(i*10); //更高位数字
                int low=(n%i);  //更低位数字
                int cur=(n/i)%10;  //当前位数字
                if(cur==0){
                    count+=high*i;
                }else if(cur==1){
                    count+=high*i+(low+1);
                }else{
                    count+=(high+1)*i;
                }
            }
            return count;
        }
    }
    

## **收获**

1.找规律要耐心！欲速则不达。

2.学会提取不同位置的数字，以及更高、更低位置的数字；学会遍历每个位数的循环。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)