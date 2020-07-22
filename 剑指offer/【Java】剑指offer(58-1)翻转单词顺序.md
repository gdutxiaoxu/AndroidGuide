# 【Java】 剑指offer(58-1) 翻转单词顺序  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student.
"，则输出"student. a am I"。

## 思路

一开始自己觉得要用split()方法，但这要开辟新的数组，占内存空间，不行。 **  
**

首先实现翻转整个句子：只需要在首尾两端各放置一个指针，交换指针所指的数字，两端指针往中间移动即可。之后根据空格的位置，对每个单词使用同样的方法翻转即可。

**测试算例** ****

1.功能测试（句子中有一个/多个单词，空格在开头、中间、结尾）

2.边界值测试（null，空字符串，句子全为空格）

## **Java代码**

    
    
    //题目：输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。
    //为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，
    //则输出"student. a am I"。
    
    public class ReverseWordsInSentence {
        public String ReverseSentence(char[] chars) {
            if(chars==null || chars.length<=0)
                return String.valueOf(chars);
            //翻转整个句子
            reverseSb(chars,0,chars.length-1);
            //翻转单词（指针指向单词的第一个和最后一个）
            int start=0;
            int end=0;
            while(start<chars.length){
                while(end<chars.length && chars[end]!=' ')
                    end++;
                reverseSb(chars,start,end-1);
                start=++end;
            }
            /*翻转单词的另一种写法（指针指向blank位置）
            int blank = -1;
            for(int i = 0;i < chars.length;i++){
                if(chars[i] == ' '){ 
                    int nextBlank = i;
                    reverse(chars,blank + 1,nextBlank - 1);
                    blank = nextBlank;
                }
            }
            reverse(chars,blank + 1,chars.length - 1);//最后一个单词单独进行反转
            */
            return String.valueOf(chars);
        }
        
        private void reverseSb(char[] chars,int start,int end){
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

1.翻转字符串方法get√

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)