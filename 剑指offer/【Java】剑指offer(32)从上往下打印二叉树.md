# 【Java】 剑指offer(32) 从上往下打印二叉树  
  
> 作者:gdutxiaoxu<br/> 微信公众号:徐公码字（stormjun94）<br/>来源:https://github.com/gdutxiaoxu/Android_interview

本文参考自《剑指offer》一书，代码采用Java语言。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

## 题目

（一）从上往下打印出二叉树的每个结点，同一层的结点按照从左到右的顺序打印。

（二）从上到下按层打印二叉树，同一层的结点按从左到右的顺序打印，每一层打印到一行。

（三）请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

## 思路

（一）不分行从上往下打印二叉树：该题即为对二叉树的层序遍历，结点满足先进先出的原则，采用队列。每从队列中取出头部结点并打印，若其有子结点，把子结点放入队列尾部，直到所有结点打印完毕。

    
    
    	/*
    	 * 不分行从上往下打印二叉树
    	 */
    	// 题目：从上往下打印出二叉树的每个结点，同一层的结点按照从左到右的顺序打印。
    	public void printTree1(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		while (queue.size()!=0) {
    			node = queue.poll();
    			System.out.print(node.val + " ");
    			if (node.left != null)
    				queue.offer(node.left);
    			if (node.right != null)
    				queue.offer(node.right);
    		}
    		System.out.println();
    	}
    

（二）分行从上到下打印二叉树：同样使用队列，但比第一题增加两个变量：当前层结点数目pCount，下一层结点数目nextCount。根据当前层结点数目来打印当前层结点，同时计算下一层结点数目，之后令pCount等于nextCount，重复循环，直到打印完毕。

    
    
    	/*
    	 * 分行从上到下打印二叉树
    	 */
    	// 题目：从上到下按层打印二叉树，同一层的结点按从左到右的顺序打印，每一层
    	// 打印到一行。
    	public void printTree2(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		int pCount = 0;		 //当前层结点数目
    		int nextCount = 1;   //下一层结点数目
    		while (!queue.isEmpty()) {
    			pCount = nextCount;
    			nextCount = 0;
    			//打印当前层数字，并计算下一层结点数目
    			for (int i = 1; i <= pCount; i++) {
    				node = queue.poll();
    				System.out.print(node.val + " ");
    				if (node.left != null) {
    					queue.offer(node.left);
    					nextCount++;
    				}
    				if (node.right != null) {
    					queue.offer(node.right);
    					nextCount++;
    				}
    			}
    			System.out.println();
    		}
    	}
    

（三）之字形打印二叉树：

（1）自己开始想的方法：在（二）的基础上，多定义一个表示当前层数的变量level。每层结点不直接打印，放入一个数组中，根据此时的层数level的奇偶来决定正向还是反向打印数组。

    
    
    	/*
    	 * 之字形打印二叉树
    	 */
    	// 题目：请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺
    	// 序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，
    	// 其他行以此类推。
    	/**
    	 * 自己开始想的方法，采用数组存储每层的数字，根据当前层数确定正反向打印数组
    	 */
    	public void printTree3_1(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		int pCount = 0;		 //当前层结点数目
    		int nextCount = 1;   //下一层结点数目
    		int level=1;    //层数
    		int[] pNums=null;    //用于存储当前层的数字
    		while (!queue.isEmpty()) {
    			pCount = nextCount;
    			nextCount = 0;
    			pNums=new int[pCount];
    			//存储当前层数字，并计算下一层结点数目
    			for (int i = 0; i < pCount; i++) {
    				node = queue.poll();
    				pNums[i]=node.val;
    				if (node.left != null) {
    					queue.offer(node.left);
    					nextCount++;
    				}
    				if (node.right != null) {
    					queue.offer(node.right);
    					nextCount++;
    				}
    			}
    			//根据当前层数确定正向或者反向打印数组
    			if((level&1)!=0 ) {
    				for(int i=0;i<pCount;i++) {
    					System.out.print(pNums[i]+" ");
    				}
    			}else {
    				for(int i=pCount-1;i>=0;i--) {
    					System.out.print(pNums[i]+" ");
    				}
    			}
    			level++;
    			System.out.println();
    		}
    	}
    

（2）书中提供的方法：采用两个栈，对于不同层的结点，一个栈用于正向存储，一个栈用于逆向存储，打印出来就正好是相反方向。

    
    
    	/**
    	 * 采用两个栈进行操作的方法
    	 */
    	public void printTree3_2(TreeNode root) {
    		if (root == null)
    			return;
    		Stack<TreeNode> stack1 = new Stack<TreeNode>();
    		Stack<TreeNode> stack2 = new Stack<TreeNode>();
    		TreeNode node = null;
    		stack1.push(root);
    		while(!stack1.empty() || !stack2.empty()) {
    			while(!stack1.empty()) {
    				node=stack1.pop();
    				System.out.print(node.val + " ");
    				if (node.left != null)
    					stack2.push(node.left);
    				if (node.right != null)
    					stack2.push(node.right);
    			}
    			System.out.println();
    			while(!stack2.empty()) {
    				node=stack2.pop();
    				System.out.print(node.val + " ");
    				if (node.right != null)
    					stack1.push(node.right);
    				if (node.left != null)
    					stack1.push(node.left);
    			}
    			System.out.println();
    		}
    	}
    

**测试算例** ****

1.功能测试（完全二叉树；左斜树；右斜树）

2.特殊测试（null；一个结点）

## **完整Java代码**

含测试代码：

    
    
    import java.util.LinkedList;
    import java.util.Stack;
    /**
     * 
     * @Description 面试题32：从上往下打印二叉树
     *
     * @author yongh
     */
    
    public class PrintTreeFromTopToBottom {
    	public class TreeNode {
    		int val = 0;
    		TreeNode left = null;
    		TreeNode right = null;
    
    		public TreeNode(int val) {
    			this.val = val;
    		}
    	}
    	
    	
    	/*
    	 * 	不分行从上往下打印二叉树
    	 */
    	// 题目：从上往下打印出二叉树的每个结点，同一层的结点按照从左到右的顺序打印。
    	public void printTree1(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		while (queue.size()!=0) {
    			node = queue.poll();
    			System.out.print(node.val + " ");
    			if (node.left != null)
    				queue.offer(node.left);
    			if (node.right != null)
    				queue.offer(node.right);
    		}
    		System.out.println();
    	}	
    
    	/*
    	 * 分行从上到下打印二叉树
    	 */
    	// 题目：从上到下按层打印二叉树，同一层的结点按从左到右的顺序打印，每一层
    	// 打印到一行。
    	public void printTree2(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		int pCount = 0;		 //当前层结点数目
    		int nextCount = 1;   //下一层结点数目
    		while (!queue.isEmpty()) {
    			pCount = nextCount;
    			nextCount = 0;
    			//打印当前层数字，并计算下一层结点数目
    			for (int i = 1; i <= pCount; i++) {
    				node = queue.poll();
    				System.out.print(node.val + " ");
    				if (node.left != null) {
    					queue.offer(node.left);
    					nextCount++;
    				}
    				if (node.right != null) {
    					queue.offer(node.right);
    					nextCount++;
    				}
    			}
    			System.out.println();
    		}
    	}
    	
    	/*
    	 * 之字形打印二叉树
    	 */
    	// 题目：请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺
    	// 序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，
    	// 其他行以此类推。
    	/**
    	 * 自己开始想的方法，采用数组存储每层的数字，根据当前层数确定正反向打印数组
    	 */
    	public void printTree3_1(TreeNode root) {
    		if (root == null)
    			return;
    		LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    		queue.offer(root);
    		TreeNode node = null;
    		int pCount = 0;		 //当前层结点数目
    		int nextCount = 1;   //下一层结点数目
    		int level=1;    //层数
    		int[] pNums=null;    //用于存储当前层的数字
    		while (!queue.isEmpty()) {
    			pCount = nextCount;
    			nextCount = 0;
    			pNums=new int[pCount];
    			//存储当前层数字，并计算下一层结点数目
    			for (int i = 0; i < pCount; i++) {
    				node = queue.poll();
    				pNums[i]=node.val;
    				if (node.left != null) {
    					queue.offer(node.left);
    					nextCount++;
    				}
    				if (node.right != null) {
    					queue.offer(node.right);
    					nextCount++;
    				}
    			}
    			//根据当前层数确定正向或者反向打印数组
    			if((level&1)!=0 ) {
    				for(int i=0;i<pCount;i++) {
    					System.out.print(pNums[i]+" ");
    				}
    			}else {
    				for(int i=pCount-1;i>=0;i--) {
    					System.out.print(pNums[i]+" ");
    				}
    			}
    			level++;
    			System.out.println();
    		}
    	}
    	
    	/**
    	 * 采用两个栈进行操作的方法
    	 */
    	public void printTree3_2(TreeNode root) {
    		if (root == null)
    			return;
    		Stack<TreeNode> stack1 = new Stack<TreeNode>();
    		Stack<TreeNode> stack2 = new Stack<TreeNode>();
    		TreeNode node = null;
    		stack1.push(root);
    		while(!stack1.empty() || !stack2.empty()) {
    			while(!stack1.empty()) {
    				node=stack1.pop();
    				System.out.print(node.val + " ");
    				if (node.left != null)
    					stack2.push(node.left);
    				if (node.right != null)
    					stack2.push(node.right);
    			}
    			System.out.println();
    			while(!stack2.empty()) {
    				node=stack2.pop();
    				System.out.print(node.val + " ");
    				if (node.right != null)
    					stack1.push(node.right);
    				if (node.left != null)
    					stack1.push(node.left);
    			}
    			System.out.println();
    		}
    	}
    
    	//============测试代码==============
    	private void test(int testNum,TreeNode root) {
    		System.out.println("=========test"+testNum+"===========");
    		System.out.println("method1:");
    		printTree1(root);
    		System.out.println("method2:");
    		printTree2(root);
    		System.out.println("method3_1:");
    		printTree3_1(root);
    		System.out.println("method3_2:");
    		printTree3_2(root);
    	}
    	
    	//null
    	private void test1() {
    		TreeNode node=null;
    		test(1, node);
    	}
    	
    	//单个结点
    	private void test2() {
    		TreeNode node=new TreeNode(1);
    		test(2, node);
    	}
    	
    	//左斜
    	private void test3() {
    		TreeNode node1=new TreeNode(1);
    		TreeNode node2=new TreeNode(2);
    		TreeNode node3=new TreeNode(3);
    		node1.left=node2;
    		node2.left=node3;
    		test(3, node1);
    	}
    	
    	//右斜
    	private void test4() {
    		TreeNode node1=new TreeNode(1);
    		TreeNode node2=new TreeNode(2);
    		TreeNode node3=new TreeNode(3);
    		node1.right=node2;
    		node2.right=node3;
    		test(4, node1);
    	}
    	
    	//完全二叉树
    	private void test5() {
    		TreeNode[] nodes = new TreeNode[15];
    		for(int i=0;i<15;i++) {
    			nodes[i]= new TreeNode(i+1);
    		}
    		for(int i=0;i<7;i++) {
    			nodes[i].left=nodes[2*i+1];
    			nodes[i].right=nodes[2*i+2];
    		}
    		test(5, nodes[0]);
    	}
    	
    	public static void main(String[] args) {
    		PrintTreeFromTopToBottom demo= new PrintTreeFromTopToBottom();
    		demo.test1();
    		demo.test2();
    		demo.test3();
    		demo.test4();
    		demo.test5();
    	}
    }
    

![](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif)![](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

    
    
    =========test1===========
    method1:
    method2:
    method3_1:
    method3_2:
    =========test2===========
    method1:
    1 
    method2:
    1 
    method3_1:
    1 
    method3_2:
    1 
    
    =========test3===========
    method1:
    1 2 3 
    method2:
    1 
    2 
    3 
    method3_1:
    1 
    2 
    3 
    method3_2:
    1 
    2 
    3 
    
    =========test4===========
    method1:
    1 2 3 
    method2:
    1 
    2 
    3 
    method3_1:
    1 
    2 
    3 
    method3_2:
    1 
    2 
    3 
    
    =========test5===========
    method1:
    1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 
    method2:
    1 
    2 3 
    4 5 6 7 
    8 9 10 11 12 13 14 15 
    method3_1:
    1 
    3 2 
    4 5 6 7 
    15 14 13 12 11 10 9 8 
    method3_2:
    1 
    3 2 
    4 5 6 7 
    15 14 13 12 11 10 9 8 

PrintTreeFromTopToBottom

## **收获**

1.层序遍历时，一般都要用到队列，可以用LinkedList类（方法：poll() 和 offer(Obj) ）。

2.在分行打印时，定义的两个int有明显实际意义（当前层结点数目，下一层结点数目）。自己编程时，一开始只知道要设置两个变量，但没有去想这两个变量的实际意义。当明白变量意义时，自己的思路会更清晰，而且代码可读性也更好。

**更多《剑指Offer》Java实现合集:https://github.com/gdutxiaoxu/Android_interview ******

扫一扫，关注我的微信公众号徐公码字（stormjun94），一起敲代码，一起吹水，书写属于自己的人生。

![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)