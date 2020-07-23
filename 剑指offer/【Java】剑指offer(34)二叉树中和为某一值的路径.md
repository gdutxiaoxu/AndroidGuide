# 【Java】 剑指offer(34) 二叉树中和为某一值的路径  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一棵二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

## 思路

1.假设找到了其中一条路径，达到叶结点后，由于没有指向父结点的指针，所以必须 **提前创建一个链表** 存储前面经过的结点。

2.由于是从根结点出发，所以要想到使用 **前序遍历**

3.利用链表存储结点，在该结点完成左右子树的路径搜索后（即递归函数结束，返回到其父结点之前），要 **删除该结点** ，从而记录别的路径。

**具体实现：**
通过前序遍历，从根结点出发，每次在链表中存储遍历到的结点，若到达叶子结点，则根据所有结点的和是否等于输入的整数，判断是否打印输出。在当前结点访问结束后，递归函数将会返回到它的父结点，所以在函数退出之前，要删除链表中的当前结点，以确保返回父结点时，储存的路径刚好是从根结点到父结点。

**改进：**
书中的代码是根据所有结点的和是否等于输入的整数，判断是否打印输出。其实没有这个必要，只需要在每次遍历到一个结点时，令目标整数等于自己减去当前结点的值，若到达根结点时，最终的目标整数等于0就可以打印输出。（描述得不是很清楚，就是相当于每个结点的目标整数不同，详见代码）

**测试算例** ****

1.功能测试（一条或者多条对应路径；无对应路径；结点值为正负零；）

2.特殊测试（根结点为null）

## **Java代码**

    
    
    //题目：输入一棵二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所
    //有路径。从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。
    
    public class PathInTree {
    	public class TreeNode {
    	    int val = 0;
    	    TreeNode left = null;
    	    TreeNode right = null;
    	    public TreeNode(int val) {
    	        this.val = val;
    	    }
    	}
    	
    	public void findPath(TreeNode root,int target) {
    		if(root==null)
    			return;
    		ArrayList<Integer> list= new ArrayList<>();
    		printPath(root, target,list);
    	}
    	
    	private void printPath(TreeNode node,int target,ArrayList<Integer> list) {
    		if(node==null)
    			return;
    		list.add(node.val);
    		target-=node.val;  //每个结点的target不会受到方法的影响而改变
    		if(target==0 && node.left==null && node.right==null) {  //叶子结点
    				for (Integer integer : list)
    					System.out.print(integer+" ");
    				System.out.println();
    		}else {		//中间结点
    			printPath(node.left, target, list);
    			printPath(node.right, target, list);
    		}
    		list.remove(list.size()-1);
    	}
    

牛客网中题目:https://www.nowcoder.com/questionTerminal/b736e784e3e34731af99065031301bca?toCommentId=2213961有多两点要求：1.返回类型为ArrayList<ArrayList<Integer>>，即返回所有路径的集合；2.要求返回的集合中，长度大的靠前。下面是实现的代码：

    
    
    /*
     * 几个要点：
     * 1. 将nodeList和pathList定义成全局变量，避免在方法中的多次传递
     * 2. 在pathList中添加nodeList时，因为nodeList会不断变化，所以必须新建一个list存入
     *    复制ArrayList的方法：newList=new ArrayList<Integer>(oldList)(复制内容，而不是复制地址，注意与newList=oldList的区分）
     * 3. 在当前结点完成左右子树的路径搜索后，记得删除nodeList中的当前结点
     * 4. target是基本数据类型int，不会受到方法的影响而改变
     */
    private ArrayList<Integer> nodeList= new ArrayList<>();
    private ArrayList<ArrayList<Integer>> pathList = new ArrayList<>();
     
    public ArrayList<ArrayList<Integer>> FindPath(TreeNode node,int target) {
        if(node==null)
            return pathList;
        nodeList.add(node.val);
        target-=node.val;
        if(target==0 && node.left==null && node.right==null) {  //叶子结点
            //长度大的nodeList插入到pathList的前面
            int i=0;
            while(i<pathList.size() && nodeList.size()<pathList.get(i).size() ) //记得防止越界
                    i++;
            pathList.add(i, new ArrayList<Integer>(nodeList));  //nodeList会随方法变化，必须新建一个list存入pathList中！
        }else {  //不是叶子结点
            pathList=FindPath(node.left, target);
            pathList=FindPath(node.right, target);
        }
        nodeList.remove(nodeList.size()-1);  //记得删除当前结点
        return pathList;
    }
    

## **收获**

1.二叉树的许多题目与遍历（包括层序遍历）有关，要深刻理解；根据根结点的位置判断使用哪一种遍历。

2.二叉树遍历过程没有父结点指针，要保存路径的话，必须要创建容器存储之前的结点。

3.熟悉这道题中在每次递归函数结束前删除当前结点的操作，这可以确保返回到父结点时路径刚好是从根结点到父结点。

4.target-=node.val这句代码非常好，多多体会。

5.牛客网的那部分代码：在链表中存储一个对象时，如果该对象是不断变化的，则应该创建一个新的对象复制该对象的内容（而不是指向同一个对象），将这个新的对象存储到链表中。。如果直接存储该对象的话，链表中的对象也会不断变化。基本数据类型和String则没有这种问题。说到底其实是存储的是地址还是值的问题这篇文章:https://www.cnblogs.com/yongh/p/9821916.html讨论了一下。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)