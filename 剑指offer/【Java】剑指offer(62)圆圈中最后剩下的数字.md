# 【Java】 剑指offer(62) 圆圈中最后剩下的数字  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

0, 1, …, n-1这n个数字排成一个圆圈，从数字0开始每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。

## 思路

**方法一** ：采用链表来存放数据，每次对长度取余来实现循环

将所有数字放入LinkedList链表中（LinkedList比ArrayList更适合增删操作）。假设当前删除的结点下标为removeIndex，则下一个要删除的结点的下标为：(removeIndex+m-1)%list.size()，通过取余符号可以实现类型循环的操作。

注：没必要用循环链表，反而会更麻烦了。

**方法二：** 数学推导规律

n个数字的圆圈，不断删除第m个数字，我们把 **最后剩下的数字** 记为 **f(n,m)** 。

n个数字中第一个被删除的数字是(m-1)%n， 我们记作k， **k=(m-1)%n** 。

那么剩下的n-1个数字就变成了：0,1,……k-1,k+1,……,n-1，我们把下一轮第一个数字排在最前面，并且将这个长度为n-1的数组映射到0~n-2。

原始数字：k+1,……, n-1, 0, 1,……k-1

映射数字：0 ,……,n-k-2, n-k-1, n-k,……n-2

把映射数字记为x，原始数字记为y，那么映射数字变回原始数字的公式为 **y=(x+k+1)%n** 。

在映射数字中，n-1个数字，不断删除第m个数字，由定义可以知道，最后剩下的数字为 **f(n-1,m)**
。我们把它变回原始数字，由上一个公式可以得到最后剩下的原始数字是 **（ **f(n-1,m)**
+k+1)%n，**而这个数字就是也就是一开始我们标记为的 **f(n,m)** ，所以可以推得递归公式如下：

****f(n,m) = **（ **f(n-1,m)** +k+1)%n******

将 ** ** ** **k=(m-1)%n******** 代入，化简得到：

************f(n,m) = **（ **f(n-1,m)** +m)%n**************

**************************f(1,m) = 0**************************

************ 代码中可以采用循环或者递归的方法实现该递归公式。时间复杂度为 **O(n)** ，空间复杂度为 **O(1)** 。

**测试算例** ****

1.功能测试（m大于/小于/等于n）

2.特殊测试（n、m <=0）

3.性能测试（n=4000,n=997）

## **Java代码**

    
    
    //题目：0, 1, …, n-1这n个数字排成一个圆圈，从数字0开始每次从这个圆圈里
    //删除第m个数字。求出这个圆圈里剩下的最后一个数字。
    
    public class LastNumberInCircle {
        /*
         * 方法一：采用推导出来的方法
         */
        public int LastRemaining_Solution(int n, int m) {
            if(n<1 || m<1)
                return -1; //出错
            int last=0;
            for(int i=2;i<=n;i++){
                last=(last+m)% i;  //这里是i不是n！！！
            }
            return last;
        }
        
        /*
         * 方法二：采用链表来存放，每次对长度取余来实现循环
         */
        public int LastRemaining_Solution2(int n, int m) {
            if(n<1 || m<1)
                return -1; //出错
            LinkedList<Integer> list = new LinkedList<Integer>();
            for(int i=0;i<n;i++)
                list.add(i);
            int removeIndex=0;
            while(list.size()>1){
                removeIndex=(removeIndex+m-1)%list.size();
                list.remove(removeIndex);
            }
            return list.getFirst();
        }
    }
    

## **收获**

1.对于下标循环一圈类似的问题，通过%可以很好地实现循环，而不需要我们自己构造循环链表；

2.(a%n+b)%n=(a+b)%n

3.尽量学会本题的数学方法，特别是要掌握好数字间映射的方法。

4.公式法中，`last=(last+m)% i; ``//这里是i不是n！！！`

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)