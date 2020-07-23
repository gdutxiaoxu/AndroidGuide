# 【Java】 剑指offer(58-2) 左旋转字符串  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如输入字符串"abcdefg"和数字2，该函数将返回左旋转2位得到的结果"cdefgab"。

## 思路

最初的想法是令chars[i] =
chars[i+n]，将后面的数字都往前移，最后面空出的位置放入前面的数字，如abcdef，n=2时，将c放入a的位置，e放入c的位置，a放入e的位置，b也同理，就可以得到cdefab了。但是这没有考虑到最后空出的位置是否正确，例如abcdefg中，同样的方法将会得到cdeba，答案错误，就是因为后面的位置对应不上。思路错误！

正确思路：本题思路和上一道翻转单词顺序:https://www.cnblogs.com/yongh/p/9963135.html的原理一模一样，只是上一道题有空格，这道题没空格，其实这道题还更简单。先分别翻转前半部分字符串和后半部分字符串，最后翻转整个字符串即可。

**测试算例** ****

1.功能测试（对长度为n的字符串，左旋转-1,0,1,2,n-1,n,n+1位）

2.边界值测试（null）

## **Java代码**

    
    
    //题目：字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。
    //请定义一个函数实现字符串左旋转操作的功能。比如输入字符串"abcdefg"和数
    //字2，该函数将返回左旋转2位得到的结果"cdefgab"。
    
    public class LeftRotateString {
        public String leftRotateString(char[] chars,int n) {
            if(chars==null ||chars.length<=0)
                return String.valueOf(chars);
            if(n<=0 || n>chars.length)
                return String.valueOf(chars); 
            reverse(chars,0,n-1);
            reverse(chars,n,chars.length-1);
            reverse(chars,0,chars.length-1);
            return String.valueOf(chars);
        }
        
        private void reverse(char[] chars, int start,int end){
            while(start<end){
                char temp=chars[start];
                chars[start]=chars[end];
                chars[end]=temp;
                start++;
                end--;
            }
        }
    }
    

## **收获**

1.这道题看似是移动字符，其实是翻转字符串实现的，要记住这类方法。知识迁移能力呀！

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)