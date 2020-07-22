# 【Java】 剑指offer(45) 把数组排成最小的数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3, 32,
321}，则打印出这3个数字能排成的最小数字321323。

## 思路

不好的方法：求出所有全排列（类字符串的排列:https://www.cnblogs.com/yongh/p/9869719.html
），将数字拼起来，最后求出所有的最小值。这效率太低，且没有考虑到大数问题。

好的方法：观察规律，自行定义一种排序规则。

对于数字m和n，可以拼接成mn和nm，如果mn <nm，我们定义m小于n。反之则相反。利用这个排序规则，从小排到大即可实现题目要求。

拼接m和n时，要考虑到大数问题，因此将m和n拼接起来的数字转换成字符串处理。因为mn和nm的字符串位数相同，因此它们的大小只需要按照字符串大小的比较规则就可以了。

具体实现：将数字存入ArrayList中，通过利用Collections.` **sort** (List<T> list, Comparator<?
super T> c)`方法进行排序。Comparator中重写compar()方法来规定比较规则。

**测试算例** ****

1.功能测试（1个数字；多个数字；数字数位有重复）

2.特殊测试（null）

## **Java代码**

    
    
    //题目：输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼
    //接出的所有数字中最小的一个。例如输入数组{3, 32, 321}，则打印出这3个数
    //字能排成的最小数字321323。
    
    public class SortArrayForMinNumber {
        public String PrintMinNumber(int [] numbers) {
            if(numbers==null || numbers.length<=0)
                return "";
            ArrayList<String> list = new ArrayList<String>();
            for(int number:numbers)
                list.add(String.valueOf(number));
            Collections.sort(list,new Comparator<String>(){
                @Override
                public int compare(String s1,String s2){
                    String a=s1+s2;
                    String b=s2+s1;
                    return a.compareTo(b);
                }
            });
            StringBuilder sb= new StringBuilder();
            for(String str:list)
                sb.append(str);
            return sb.toString();
        }
    }
    

## **收获**

1.记住Collections.` (List<T> list, Comparator<? super T> c)在重写compare()方法的使用。`

2.小心大数问题，用字符串解决大数问题。

3.遇到类似排序问题，想想自定排序规则是否更加方便。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)