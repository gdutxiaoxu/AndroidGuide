# 【Java】 剑指offer(29) 顺时针打印矩阵  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

## 思路

每次打印矩阵最外面的一圈（用方法printMatrixInCircle()表示），每次都是这个操作，所以可以采用递归。每次打印矩阵的左上角的横纵坐标相同，即为start，而其余三个角的坐标都与行列数以及start有关，因此只需要for循环即可实现打印。

当然，其实只要针对start进行循环判断， start*2的值小于行数和列数时才需要继续打印，这样，通过这个条件，可以用循环来打印每次的最外圈矩阵。

**测试算例** ****

多行多列，单行多列，多行单列，一个数的矩阵，空矩阵，null

## **Java代码**

    
    
    //题目：输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
    
    public class PrintMatrix {
    	public void printMatrix(int[][] matrix) {
    		if(matrix==null || matrix.length<=0)
    			return;
    		printMatrixInCircle(matrix, 0);
    	}	
    	
    	private void printMatrixInCircle(int[][] matrix,int start) {
    		int row=matrix.length;
    		int col=matrix[0].length;
    		int endX=col-1-start;
    		int endY=row-1-start;
    		if(endX<start || endY<start)
    			return;
    		//仅一行
    		if(endY==start) {
    			for(int i=start;i<=endX;i++) {
    				System.out.print(matrix[start][i]+" ");
    			}
    			return;  //记得结束
    		}
    		//仅一列
    		if(endX==start) {
    			for(int i=start;i<=endY;i++) {
    				System.out.print(matrix[i][start]+" ");
    			}
    			return;  //记得结束
    		}				
    		
    		//打印边界
    		for(int i=start;i<=endX;i++) {
    			System.out.print(matrix[start][i]+" ");
    		}
    		for(int i=start+1;i<=endY;i++) {
    			System.out.print(matrix[i][endX]+" ");
    		}
    		for(int i=endX-1;i>=start;i--) {
    			System.out.print(matrix[endY][i]+" ");
    		}
    		for(int i=endY-1;i>=start+1;i--) {
    			System.out.print(matrix[i][start]+" ");
    		}
    		
    		//继续打印更内部的矩阵，令start+1
    		printMatrixInCircle(matrix, start+1);
    	}
    	
    	
    	public static void main(String[] args) {
    		PrintMatrix demo = new PrintMatrix();
    		int[][] a= {{1,2,3,4},{5,6,7,8},{9,10,11,12},{13,14,15,16}};
    //		int[][] a= {};
    //		int[][] a= {{}};
    //		int[][] a= {{1}};
    //		int[][] a= {{1,2,3,4}};
    //		int[][] a= {{1},{2},{3},{4}};
    //		int[][] a= {{1,2,3},{4,5,6}};
    //		int[][] a=null;
    		demo.printMatrix(a);
    	}
    

下面的代码是来牛客网:https://www.nowcoder.com/questionTerminal/9b4c81a02cd34f76be2659fa0d54342a的C++代码：1.采用的是循环；2.在打印一圈时，单行或者单列情况只需要在从右往左打印和从下往上打印时判断是否会出现重复打印（即后面两个for循环）。代码比较简洁。

    
    
    /*解题思路：顺时针打印就是按圈数循环打印，一圈包含两行或者两列，在打印的时候会
    出现某一圈中只包含一行，要判断从左向右打印和从右向左打印的时候是否会出现重复打印，
    同样只包含一列时，要判断从上向下打印和从下向上打印的时候是否会出现重复打印的情况*/
    class Solution {
    public:
        vector<int> printMatrix(vector<vector<int> > matrix) {
            vector<int>res;
            res.clear();
            int row=matrix.size();//行数
            int collor=matrix[0].size();//列数
            //计算打印的圈数
            int circle=((row<collor?row:collor)-1)/2+1;//圈数
            for(int i=0;i<circle;i++){
                //从左向右打印
                for(int j=i;j<collor-i;j++)
                    res.push_back(matrix[i][j]);         
                //从上往下的每一列数据
                for(int k=i+1;k<row-i;k++)
                    res.push_back(matrix[k][collor-1-i]);
                //判断是否会重复打印(从右向左的每行数据)
                for(int m=collor-i-2;(m>=i)&&(row-i-1!=i);m--)
                    res.push_back(matrix[row-i-1][m]);
                //判断是否会重复打印(从下往上的每一列数据)
                for(int n=row-i-2;(n>i)&&(collor-i-1!=i);n--)
                    res.push_back(matrix[n][i]);}
            return res;
        }
    };
    

## **收获**

1.打印一圈矩阵时，注意单行或者单列时是否会重复打印。

2.每一圈矩阵左上角的横纵坐标相等，其余三个角的坐标可以由左上角坐标获得。

3.打印矩阵的圈数与其列数或者行数的一半有关。简单但要能想到。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)