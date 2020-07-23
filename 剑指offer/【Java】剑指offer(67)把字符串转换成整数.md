# 【Java】 剑指offer(67) 把字符串转换成整数  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

****

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请你写一个函数StrToInt，实现把字符串转换成整数这个功能。当然，不能使用atoi或者其他类似的库函数。

## 思路

题目很简单，主要就是实现对每个字符转化为数字，并进行累加即可。但是有很多特殊情况都需要考虑进去，例如null、空字符串、带有正负号、字符不是数字、溢出等等。

对于非法的特殊输入，返回值为0，还要用一个全局变量进行标记。

写代码时一定要考虑清楚各种测试用例。

**测试用例**

1.功能测试（正、负、零、带有正负号的数字）

2.边界值测试（最大正整数，最小负整数）

3.特殊测试（null，数空字符串，仅有正负号，非法字符）

## **Java代码**

今天脑子有点乱，代码总感觉不是很简洁，有点繁琐，但功能是完善的。

附注:字符串如果仅有正负号这里认定为非法输入

    
    
    //题目：请你写一个函数StrToInt，实现把字符串转换成整数这个功能。当然，不
    //能使用atoi或者其他类似的库函数。
    
    public class StringToInt {
        static boolean isValid = false;
        public static int strToInt(String str) {
            if(str == null || str.length()<=0)
                return 0;
            char[] chars = str.toCharArray();
            long num=0;  //先用long来存储，以防止越界
            boolean minus=false;
            for(int i=0; i<chars.length; i++){
                if(i==0 && chars[i]=='-'){
                    minus=true;
                }else if(i==0 && chars[i]=='+'){
                    minus=false;
                }else{
                    int a=(int) (chars[i]-'0');
                    if(a<0 || a>9){
                        isValid=false;
                        return 0;
                    }
                    num= (minus==false) ? num*10+a : num*10-a;
                    isValid=true;  //不放在最后面是为了防止str=‘+’的情况被判断为true
                    if((!minus && num>0x7FFFFFFF)
                       ||(minus && num<0x80000000)){
                        isValid=false;
                        return 0;
                    }
                }
            }
            return (int)num;
        }
        
        //简单测试下
        public static void main(String[] args) {
    		System.out.println(strToInt("1948243")==1948243);
    		System.out.println(isValid==true);
    		System.out.println(strToInt("+1948243")==1948243);
    		System.out.println(isValid==true);
    		System.out.println(strToInt("-1948243")==-1948243);
    		System.out.println(isValid==true);
    		System.out.println(strToInt("-0")==0);
    		System.out.println(isValid==true);
    		System.out.println(strToInt("-194+8243")==0);
    		System.out.println(isValid==false);
    		System.out.println(strToInt("")==0);
    		System.out.println(isValid==false);
    		System.out.println(strToInt(null)==0);
    		System.out.println(isValid==false);
    		System.out.println(strToInt("999999999999999")==0);
    		System.out.println(isValid==false);
    		System.out.println(strToInt("+")==0);
    		System.out.println(isValid==false);
    		
    		System.out.println(strToInt("2147483647")==2147483647); //0x7FFFFFFF
    		System.out.println(isValid==true);
    		System.out.println(strToInt("2147483648")==0);
    		System.out.println(isValid==false);
    		
    		System.out.println(strToInt("-2147483648")==-2147483648); //0x80000000
    		System.out.println(isValid==true);
    		System.out.println(strToInt("-2147483649")==0);
    		System.out.println(isValid==false);
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
     true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true
    true

StringToInt

## **收获**

1.熟练掌char类型转化为int类型操作:https://www.cnblogs.com/yongh/p/9688259.html。

2.边界值测试，记住int类型最大正整数为 **0x7FFFFFFF** ，最小负整数为 **0x80000000** 。

3.注意到了负号，也要注意到正号。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)