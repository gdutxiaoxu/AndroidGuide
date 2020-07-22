# 【Java】 剑指offer(66) 构建乘积数组  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

给定一个数组A[0, 1, …, n-1]，请构建一个数组B[0, 1, …, n-1]，其中B中的元素B[i] =A[0]×A[1]×…
×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

## 思路

无法使用除法，正常连乘的话时间复杂度为 **O(n^2)** ，效率非常低。

考虑到计算每个B[i]时都会有重复，思考B[i]之间的联系，找出规律，提高效率。

![](https://img2018.cnblogs.com/blog/1407330/201811/1407330-20181116214635748-1968740855.png)

图片转构建乘积数组:https://www.cnblogs.com/wxdjss/p/5448990.html

如上图所示，可以发现：

B[i]的左半部分(红色部分)和B[i-1]有关（将B[i]的左半部分乘积看成C[i]，有C[i]=C[i-1]*A[i-1]），

B[i]的右半部分(紫色部分)与B[i+1]有关（将B[i]的右半部分乘积看成D[i]，有D[i]=D[i+1]*A[i+1]），

因此我们先从0到n-1遍历，计算每个B[i]的左半部分；
然后定义一个变量temp代表右半部分的乘积，从n-1到0遍历，令B[i]*=temp，而每次的temp与上次的temp关系即为temp*=A[i+1]。

**测试代码**

1.功能测试（正、负、零）

2.边界值测试（数组长度为2）

3.特殊测试（null，数组长度为1，0）

## **Java代码**

    
    
    //题目：给定一个数组A[0, 1, …, n-1]，请构建一个数组B[0, 1, …, n-1]，其
    //中B中的元素B[i] =A[0]×A[1]×… ×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。
    
    public class ConstuctArray {
        public int[] multiply(int[] A) {
            if(A==null || A.length<2)
                return null;
            int[] B=new int[A.length];
            B[0]=1;
            for(int i=1;i<A.length;i++)
                B[i]=B[i-1]*A[i-1];
            int temp=1;
            for(int i=A.length-2;i>=0;i--){
                temp*=A[i+1];
                B[i]*=temp;
            }
            return B;
        }
    }
    

## **收获**

1.考虑到了数组B中的元素间有关系，要进一步分析。本题就是采用画图的方法，将B看成一个矩阵，就能轻易地看出元素之间的关系了。好好学习。

2.可以直接从头到尾再从尾到头遍历，不需要创建两个临时数组C[]和D[]。自己写代码时，要尽量设计不用创建太多内存空间。

3.如果这道题可以用除法的话，记得除数不能为零！

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)