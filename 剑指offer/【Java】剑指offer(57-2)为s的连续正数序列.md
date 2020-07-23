# 【Java】 剑指offer(57-2) 为s的连续正数序列  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个正数s，打印出所有和为s的连续正数序列（至少含有两个数）。例如输入15，由于1+2+3+4+5=4+5+6=7+8=15，所以结果打印出3个连续序列1～5、4～6和7～8。

## 思路

**指针法：**

类似[(57-1) 和为s的两个数字](https://www.cnblogs.com/yongh/p/9961940.html
"发布于2018-11-15 10:15")的方法，用两个指针small和big分别代表序列的最大值和最小值。令small从1开始，big从2开始。

当从small到big的序列的和小于s时，增加big，使序列包含更多数字；（记得更新序列之和）

当从small到big的序列的和大于s时，增加small，使序列去掉较小的数字；（记得更新序列之和）

当从small到big的序列的和等于s时，此时得到一个满足题目要求的序列，输出，然后继续将small增大，往后面找新的序列。

序列最少两个数字，因此，当small到了s/2时，就可以结束判断了。

**数学分析法：**

参考牛客网](https://www.nowcoder.com/questionTerminal/c451a3fd84b64cb19485dad758a55ebe)，[丁满历险记:https://www.nowcoder.com/profile/5073898的答案。

对于一个长度为n的连续序列，如果它们的和等于s，有：

1）当n为奇数时，s/n恰好是连续序列最中间的数字，即n满足 **(n &1)==1 && s%n==0**

2）当n为偶数时，s/n恰好是连续序列中间两个数字的平均值，小数部分为0.5，即n满足 **(s%n)*2==n （** 判断条件中包含了n为偶数的判断）

得到满足条件的n后，相当于得到了序列的中间数字s/n，所以可以得到第一个数字为 **(s / n) - (n - 1) / 2**
，结合长度n可以得到所有数字。

此外，在什么范围内找n呢？我们知道n至少等于2，那至多等于多少？n最大时，序列从1开始，根据等差数列的求和公式根据等差数列的求和公式：S = (1 + n)
* n / 2，可以得到n应该小于sqrt(2s)，所以只需要从n=2到sqrt(2s)来判断满足条件的n，继而输出序列。

**测试算例** ****

1.功能测试（存在/不存在和为s的序列）

2.边界值测试（s=3）

## **Java代码**

**方法一：**

    
    
    //题目：输入一个正数s，打印出所有和为s的连续正数序列（至少含有两个数）。
    //例如输入15，由于1+2+3+4+5=4+5+6=7+8=15，所以结果打印出3个连续序列1～5、
    //4～6和7～8。
    
    public class ContinuousSquenceWithSum {
        //方法一：采用两个指针的方法
        public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
            ArrayList<ArrayList<Integer> > sequenceList = new ArrayList<ArrayList<Integer> >();
            if(sum<=0)
                return sequenceList;
            
            int small = 1;
            int big = 2;
            int curSum = small+big;
            while(small <= sum/2){
                if(curSum == sum){
                    ArrayList<Integer> sequence = new ArrayList<Integer>();
                    for(int i=small;i<=big;i++)
                        sequence.add(i);
                    sequenceList.add(sequence);
                    curSum-=small;
                    small++; //这两行位置先后要注意
                }
                if(curSum < sum){
                    big++;
                    curSum+=big;
                }
                if(curSum > sum){
                    curSum-=small;
                    small++;
                }
            }
            return sequenceList;
        }  
    }
    

方法二：

    
    
        //方法二：数学分析法
        public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
            ArrayList<ArrayList<Integer> > sequenceList = new ArrayList<ArrayList<Integer> >();
            if(sum<=0)
                return sequenceList;
            
            for(int n=(int) Math.sqrt(2*sum);n>=2;n--){
                if(((n&1)==1 && sum%n==0) || ((n&1)==0 && (sum%n)*2==n)){
                    ArrayList<Integer> sequence = new ArrayList<>();
                    for (int j = 0, k = (sum / n) - (n - 1) / 2; j < n; j++, k++) {
                        sequence.add(k);
                    }
                    sequenceList.add(sequence);
                }
            }
            return sequenceList;
        }
    

## **收获**

1.还是利用两个指针，这个技巧要学会

2.代码中求连续序列的和，并没有每次遍历计算，而是根据每次操作的情况而在之前的结果上进行加减，可以提高效率，值得学习

3.题目[57-1) 和为s的两个数字](https://www.cnblogs.com/yongh/p/9961940.html
"发布于2018-11-15 10:15")中的指针是从两端开始，本题指针从1，2开始，注意指针的初始设置。

4.方法二中，当s/n的余数为0.5时，s%n的结果是n/2，而不是1。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)