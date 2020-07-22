# 【Java】 剑指offer(3) 二维数组中的查找  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

_本文参考自《剑指offer》一书，代码采用Java语言。_

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview**

## 题目

在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## **思路**

查找整数时，如果从左上角开始查找，情况较为复杂，可以转换思路，从右上角开始查找：左边数字比较小，右边数字比较大，容易进行判断。

**测试用例**

1.要查找的数字在数组中

2.要查找的数字不在数组中

3.数组为空

4.数组不满足大小规则

5.数组每行长度不一致.

## **完整Java代码**

（含测试代码）

    
    
    /**
     * @Description 二维数组中的查找 
     *
     * @author yongh
     * @date 2018年7月16日 下午2:20:59
     */
    
    // 题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按
    // 照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个
    // 整数，判断数组中是否含有该整数。
    
    public class FindInPartiallySortedMatrix {
    
    	/*
    	 * 判断二维数组matrix中是否含有整数a
    	 * 返回值为a的下标，{-1，-1}代表不存在
    	 */
    	public int[] find(int[][] matrix, int a) {
    		int[] index = { -1, -1 };
    
    		// 判断数组是否正确
    		if (matrix == null || matrix.length <= 0) {
    			System.out.println("数组无效！");
    			return index;
    		}
    		// 判断数组数字的大小是否符合大小规则
    		int columns = matrix[0].length;
    		for (int i = 0; i < matrix.length; i++) {
    			if (matrix[i].length != columns) {
    				System.out.println("数组列数不一致！");
    				return index;
    			}
    			for (int j = 0; j < matrix[i].length; j++) {
    				if (i == 0 && j == 0)
    					// matrix[0][0]不比较
    					break;
    				if (i == 0) { // 第一行的数，仅和前一列的数比较
    					if (matrix[i][j] < matrix[i][j - 1]) {
    						System.out.println("数组中数字大小不符合要求！");
    						return index;
    					}
    				} else if (j == 0) { // 第一列的数，仅和前一行的数比较
    					if (matrix[i][j] < matrix[i - 1][j]) {
    						System.out.println("数组中数字大小不符合要求！");
    						return index;
    					}
    				} else if (matrix[i][j] < matrix[i - 1][j] || matrix[i][j] < matrix[i][j - 1]) {
    					// 其余位置的数字，和前一行或前一列的比较
    					System.out.println("数组中数字大小不符合要求！");
    					return index;
    				}
    			}
    		}
    
    		// 正式查找
    		int row = 0; // 行数
    		int column = matrix[0].length - 1; // 列数
    		while (row <= matrix.length - 1 && column >= 0) {
    			if (a == matrix[row][column]) {
    				index[0] = row;
    				index[1] = column;
    				System.out.println("数字" + a + "在二维数组中的下标为：" + index[0] + "," + index[1]); // 注意下标是从0开始的
    				return index;
    			} else if (a < matrix[row][column]) {
    				column--;
    			} else {
    				row++;
    			}
    		}
    		System.out.println("数组中不含数字：" + a);
    		return index;
    	}
    
    	// ==================================测试代码==================================
    
    	// 1 2 8 9
    	// 2 4 9 12
    	// 4 7 10 13
    	// 6 8 11 15
    	// 要查找的数在数组中
    	public void test1() {
    		System.out.print("test1：");
    		int[][] matrix = { { 1, 2, 8, 9 }, { 2, 4, 9, 12 }, { 4, 7, 10, 13 }, { 6, 8, 11, 15 } };
    		int[] index = find(matrix, 7);
    	}
    
    	// 1 2 8 9
    	// 2 4 9 12
    	// 4 7 10 13
    	// 6 8 11 15
    	// 要查找的数不在数组中
    	public void test2() {
    		System.out.print("test2：");
    		int[][] matrix = { { 1, 2, 8, 9 }, { 2, 4, 9, 12 }, { 4, 7, 10, 13 }, { 6, 8, 11, 15 } };
    		int[] index = find(matrix, 5);
    	}
    
    	// 数组为空
    	public void test3() {
    		System.out.print("test3：");
    		int[][] matrix = null;
    		int[] index = find(matrix, 7);
    	}
    
    	// 1 2 8 9
    	// 4 3 9 12
    	// 4 7 10 13
    	// 6 8 11 15
    	// 数组不满足大小规则
    	public void test4() {
    		System.out.print("test4：");
    		int[][] matrix = { { 1, 2, 8, 9 }, { 4, 3, 9, 12 }, { 4, 7, 10, 13 }, { 6, 8, 11, 15 } };
    		int[] index = find(matrix, 7);
    	}
    
    	// 数组每行长度不一致
    	public void test5() {
    		System.out.print("test5：");
    		int[][] matrix = { { 1, 2, 8 }, { 4, 3, 9, 12 }, { 4, 7, 10 }, { 6, 8, 11, 15 } };
    		int[] index = find(matrix, 7);
    	}
    
    	public static void main(String[] args) {
    		FindInPartiallySortedMatrix f = new FindInPartiallySortedMatrix();
    		f.test1(); // 注意下标是从0开始的
    		f.test2();
    		f.test3();
    		f.test4();
    		f.test5();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    test1：数字7在二维数组中的下标为：2,1
    test2：数组中不含数字：5
    test3：数组无效！
    test4：数组中数字大小不符合要求！
    test5：数组列数不一致！

FindInPartiallySortedMatrix

====================================================================

上面代码考虑了数组数字大小不符合规则的情况，所以较为繁琐。

在牛客网中提交的代码如下（不含测试代码）：

    
    
    public class Solution {
        public boolean Find(int target, int [][] array) {
            if(array==null||array.length<=0){
                return false;
            }
     
            int row=0;
            int column=array[0].length-1;
            while(row<=array.length-1 && column>=0){
                if(target==array[row][column]){
                    return true;
                }else if(target<array[row][column]){
                    column--;
                }else{
                    row++;
                }
            }
            return false;
        }
    }
    

****更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview****

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)