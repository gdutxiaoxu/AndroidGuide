# 【Java】 剑指offer(61) 扑克牌的顺子  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王可以看成任意数字。

## 思路

输入为大小等于5的数组（大小王记为0），输出为布尔值。具体步骤如下：

1）进行对5张牌进行排序；

2）找出0的个数；

3）算出相邻数字的空缺总数；

4）如果0的个数大于等于空缺总数，说明连续，反之不连续；

5）记得判断相邻数字是否相等，如果有出现相等，说明不是顺子。

**测试算例** ****

1.功能测试（没有/有一个/多个大小王，有对子，连续/不连续）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。
    //2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王可以看成任意数字。
    
    public class ContinousCards {
        public boolean isContinuous(int [] numbers) {
            if(numbers==null || numbers.length<=0)
                return false;
            Arrays.sort(numbers);
            int numberOf0 = 0;
            int numberOfGap = 0;
            for(int i=0;i<numbers.length;i++){
                if(numbers[i]==0)
                    numberOf0++;
            }
            int small = numberOf0;
            int big = numberOf0+1;
            while(big<numbers.length){
                if(numbers[small]==numbers[big])
                    return false;
                numberOfGap+=numbers[big++]-numbers[small++]-1;
            }
            if(numberOf0>=numberOfGap)  //大于等于，而不是等于！
                return true;
            return false;
        }
    }
    

## **收获**

1.这道题中，自己最开始想的是把0插入到空缺当中，当其实只要计算出0的个数和空缺的个数进行比较即可，有时候稍微转换一下思路就豁然开朗了。

2.对数组排序，采用Arrays.sort(numbers)方法（快排原理）。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)