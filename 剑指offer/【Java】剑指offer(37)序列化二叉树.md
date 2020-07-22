# 【Java】 剑指offer(37) 序列化二叉树  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

请实现两个函数，分别用来序列化和反序列化二叉树。

## 思路

一般情况下，需要采用前/后序遍历和中序遍历才能确定一个二叉树，但是其实可以只采用前序遍历（从根结点开始），将空结点(null)输出为一个特殊符号（如“$”），就可以确定一个二叉树了。

将二叉树序列化为字符串，就是前序遍历的过程，遇见空结点时，序列化为“$”，每个结点间使用逗号分隔开。

将字符串反序列化为二叉树，也使用前序遍历，遇见一个新数字(或者$)就建立一个新结点，不过需要注意的是，数字可能不只是个位数字，因此创建了一个全局Int变量index（在字符串上的移动的指针），以便于截取字符串中当前的结点值。（详见代码）

**测试算例** ****

1.功能测试（一个结点；左右斜树；完全二叉树；普通二叉树）

2.特殊测试（根结点为null）

## **Java代码**

    
    
    //题目：请实现两个函数，分别用来序列化和反序列化二叉树。
    
    public class SerializeBinaryTrees {
    	public class TreeNode {
    		int val = 0;
    		TreeNode left = null;
    		TreeNode right = null;
    
    		public TreeNode(int val) {
    			this.val = val;
    		}
    	}
    
        String Serialize(TreeNode node) {
            StringBuilder sb = new StringBuilder();
            if (node == null) {
                sb.append("$,");
            } else {
                sb.append(node.val + ",");
                sb.append(Serialize(node.left));
                sb.append(Serialize(node.right));
            }
            return sb.toString();
        }
      
        int index = 0;
        TreeNode Deserialize(String str) {
            TreeNode node = null;
            if (str == null || str.length() == 0)
                return node;
            int start = index;
            while (str.charAt(index) != ',')
                index++;
            if (!str.substring(start, index).equals("$")) {
                node = new TreeNode(Integer.parseInt(str.substring(start, index)));
                index++; // 这条语句位置别放错了
                node.left = Deserialize(str);
                node.right = Deserialize(str);
            } else {
                index++;
            }
            return node;
        }
    }
    

## **收获**

1.记住这种序列化的方式，用于表示二叉树时非常方便。

2.字符串中有分割符号时，可以对字符串采用split()方法，变为字符串数组，但是自己觉得数组的保存会消耗一定的空间，因此自己定义了全局变量index，通过substring()方法来截取每一部分的字符串。

3.字符串的比较以后尽量用equal来比较。在对某字符串采用substring()方法得到的字符串用==判断会返回false。[substring的==与equal()使用](https://www.cnblogs.com/yongh/p/9866074.html
"发布于2018-10-28 16:42")

4.String 转int 类型采用 `int` `i = Integer.parseInt( s );
不能用Integer.valueOf(s)，这返回的是Integer对象。`

5.index++的位置一定不能放错

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)