## LeetCode链表知识点&题型总结



[TOC]



>  我的 CSDN 博客:https://blog.csdn.net/gdutxiaoxu <br>
>  我的掘金：https://juejin.im/user/2207475076966584  <br>
>  github: https://github.com/gdutxiaoxu/  <br>
>  微信公众号：徐公码字(stormjun94)  <br>
>  知乎：https://www.zhihu.com/people/xujun94  <br>

## 前言

前段时间，写了面试必备的一系列文章，反应还不错。有一些读者反馈说，能不能整理一些面试常见的算法。前段时间，我恰好总结了 LeetCode 常见的面试算法题目。



[Android 面试必备 - http 与 https 协议](https://blog.csdn.net/gdutxiaoxu/article/details/97885526)

[Android 面试必备 - 计算机网络基本知识（TCP，UDP，Http，https）](https://blog.csdn.net/gdutxiaoxu/article/details/97618598)

[Android 面试必备 - 线程](https://blog.csdn.net/gdutxiaoxu/article/details/98475465)

[Android 面试必备 - JVM 及 类加载机制](https://xujun.blog.csdn.net/article/details/98896053)

[Android 面试必备 - 系统、App、Activity 启动过程](https://xujun.blog.csdn.net/article/details/99006458)

[面试官系列- 你真的了解 http 吗](https://blog.csdn.net/gdutxiaoxu/article/details/107349652)

[面试官问， https 真的安全吗，可以抓包吗，如何防止抓包吗](https://xujun.blog.csdn.net/article/details/107393249)

[java 版剑指offer算法集锦](https://juejin.im/post/6854573217038909454)

**[Android_interview github 地址](https://github.com/gdutxiaoxu/Android_interview)**



刚开始准备刷算法题目的时候，感觉真的是好难，十道题目有九道是不会的。心中曾一万只草泥马跑过，自己怎么这么辣鸡。

<img src="https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200731145019.png"/>

慢慢得，我发现算法也是一个可以通过练习慢慢成长的。


1. 首先我们要掌握基本的数据结构，数组，链表，哈希表， Set，二叉树，堆，栈等。你要知道他们有什么优缺点，适应场景是什么，时间复杂度和空间复杂度是多少。而不能知道简单的 API。
2. 接着，掌握了这些基本的数据结构之后，一些基本的算法你也要掌握以下，比如快速排序，归并排序，对排序，二分查找。这些基本的一定要掌握，面试当中经常也会问到。
3. 分类刷题，我们在力扣上面可以看到，https://leetcode-cn.com/problemset/algorithms/ ，刷题是可以按标签来的。比如链表，数组，二分查找，二叉树，动态规划等
4. 学好算法不是一日之功，需要长期的积累。建议的做法是每天做一两道题，题目不在多，贵在于理解。坚持一两个月，你会发现你的感觉逐渐好起来了



**废话不多说了，开始进入今天的正文，LeetCode链表知识点&题型总结**


## 知识点


### 什么是链表

​	链表(Linked List)是一种常见的线性结构。它不需要一块连续的内存空间，通过指针即可将一组零散的内存块串联起来。我们把内存块成为链表的节点，为了将所有的节点串起来，每个链表的节点除了存储数据之外，还需要记录链表的下一个节点的地址，这个记录下个节点地址的指针我们叫做**后驱指针**。搜索链表需要O(N)的时间复杂度，这点和数组类似，但是链表不能像数组一样，通过索引的方式以O(1)的时间读取第n个数。链表的优势在于能够以较高的效率在任意位置插入或者删除一个节点。

### 类别

#### 单向链表

​	每个节点有一个next指针指向后一个节点，还有一个成员变量用于存储数值。单向链表中有两个节点比较特殊，分别是头结点和尾节点。头结点用来记录链表的基地址，知道头结点我们就可以遍历得到整条链表。尾结点的特殊在于指针指向的是一个空指针NULL。



#### 循环链表

​	循环链表是一种特殊的单链表，与单链表不同的是尾节点不指向空地址，指向链表的头结点。优点是从链尾到链头比较方便，当要处理的数据具有环形结构特点是，非常适合用循环链表来处理。




#### 双向链表

​	双向链表支持两个方向，每个节点不只有一个后驱指针next指向后面的节点，还有一个前驱指针prev指向前面的节点。


![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200801104220.png)

#### 双向循环链表


![image](https://raw.githubusercontent.com/huxiaoman7/leetcodebook/master/Linklist/pic/4.png)

### 与数组的性能对比

| 时间复杂度 | 数组    | 链表   |
| ---- | ------------------------------------------------------------ | ------ |
| 插入删除   |O(n)| O(1) |
| 随机访问   |O(1)| O(n)|





### 优缺点

- 优点：动态扩容，不需要占用过多的内存
- 缺点：不能随机访问，如果要访问一个元素的话，不能根据索引访问，只能从头开始遍历，找到对应的元素

### 常用技巧

- 1.**使用dummy node**。dummy node就是在链表的head前加一个节点指向head，即dummy->head，可以理解成一个虚拟节点。多针对于单链表没有前向指针的问题，保证链表的head不会在删除操作中丢失。通常情况下，如果链表的head会发生变化，譬如删除或者被修改等，可以创建dummy node：

  ```java
  ListNode dummy = new ListNode(0);
  dummy.next = head;
  ```

  这样就使得操作head节点与操作其他节点没有区别。

- 2.**双指针法**。对于寻找链表的某个特定位置，或者判断是否有环等问题时，可以用两个指针变量fast和slow:

  ```java
  ListNode slow = head;
  ListNode fast = head;
  ```

  以不同的速度遍历该链表，以找到目标位置。注意：在测试时，需要分别选取链表长度为奇数和偶数的test case，可以验证算法在一般情况下的正确性避免遗漏。

- 3.**交换节点的处理**。如果需要交换两个节点的位置，譬如24题 [Swap Nodes in Pairs](https://leetcode-cn.com/problems/swap-nodes-in-pairs/),需要交换两个相邻位置的节点，对于这两个前驱节点，他们的next指针会受到影响，这两个节点本身也会受到影响，可以用以下步骤：

  - 1）先交换两个前驱节点的next指针的值
  - 2）再交换这两个节点的next指针的值

  无论这两个节点的相对位置和绝对位置如何，以上的处理方式均可成立

- 4.**同时操作两个链表的处理**。遇到这种题目，循环的条件一般可以用while（list1 && list2），当循环跳出来后，再处理剩下非空的链表，这相当于：边界情况特殊处理，常规情况常规处理。



## 题型总结

### 基本操作

#### 删除类

- 例题：19 Remove Nth Node From End of List 【Medium】
- 题意：删除链表中倒数第n个节点
- test case:

> Given ÷ list: 1->2->3->4->5, and n = 2.
>
> 删除链表中导数第二个节点，变成1->2->3->5.

- 解题思路：*双指针法* 。在head前加一个虚拟节点dummy node，并设置两个指针fast和slow。 fast指针现象前移动n个节点（从dummy节点开始移动，所以实际上是移动到了n-1位），然后fast和slow同时开始移动，当fast.next == None时，slow节点指向的就是需要删除的节点前面的一个节点，将其指向.next.next即可
- code：

Java

```java
class Solution{
public static ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;
        while(fast.next != null){
        	if(n <= 0)
        		slow = slow.next;
        	fast = fast.next;
        	n--;
        }
        if(slow.next != null)
        	slow.next = slow.next.next;
        return dummy.next;
    }
}
```




- 复杂度分析：时间复杂度O(length(list)), 即O(N)，空间复杂度O(1)

> Leetcode中包含删除类的题目：

| 序号 | 题目                                                         | 难度   | 代码 |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| 19   | [Remove   Nth Node From End of List    ](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list) | medium | java |
| 82   | [Remove   Duplicates from Sorted List II    ](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii) | Medium | java |
| 83   | [Remove   Duplicates from Sorted List    ](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list) | Easy   | java |
| 203  | [Remove   Linked List Elements    ](https://leetcode-cn.com/problems/remove-linked-list-elements) | Easy   | java |
| 237  | [Delete Node   in a Linked List    ](https://leetcode-cn.com/problems/delete-node-in-a-linked-list) | Easy   | java |



### 翻转类题型

最基础最常在面试中遇到的提醒，206一定要熟练掌握

- 例题1：206 Reverse Linked List 【easy】

- 题意：翻转一个单向链表

- test case:

  > Input：1->2->3->4->5->NULL
  >
  > Output：5->4->3->2->1->NULL

- 思考：可否用迭代和递归两种方法完成？

- 解题思路：对于翻转类的题型，我们只需要知道head->prev节点如何翻转成prev-head即可,这里我们仍然要用到dummy node，作为head的前驱节点，在翻转前，是dummy->head->2->3…->NULL,翻转后变成NULL->5->…->2->head->dummy，dummy变成了尾节点，因为这是一个单向链表，head只有一个指针，已经指向了下一个节点了，所以首先需要把head的下一个节点，即head.next用一个临时变量存储起来，与head'断开连接'，这样head就可以指向dummy了，即我们将dummy->head变成了head->dummy，第一步完成。后面的处理方式有两种写法，一种是迭代，我们可以再来用同样的方式处理head->head.next ,使之变成head.next->head，同样让head.next.next用一个变量存储起来断开与head.next的连接，然后head.next指向head即可，在这里其实head.next.next就相当于第一步中的head.next,head.next就相当于第一步的dummy,所以可以直接写成dummy = head，head = next；递归的方式则需要c创建一个递归函数，把第一步的步骤写入递归函数里面，然后再不断地调用这个递归函数即可。

- code：

  Java

  ```java
  /*迭代写法*/
  class Solution {
      public ListNode reverseList(ListNode head) {
          if (head == null || head.next == null){
              return head;
          }
          ListNode dummy = null;
          while (head != null){
              ListNode next = head.next;
              head.next = dummy;
              dummy = head;
              head = next;
          } 
          return dummy;
      }
  }
  
  
  /*递归写法*/
  class Solution{
      public ListNode reverseList(ListNode head) {
          return reverseListHelper(head, null);
      }
  
      private ListNode reverseListHelper(ListNode head, ListNode newHead) {
          if (head == null)
              return newHead;
          ListNode next = head.next;
          head.next = newHead;
          return reverseListHelper(next, head);
      }
  }
  
  ```

 

  - 复杂度分析：

    | 复杂度     | 迭代法 | 递归法 |
    | ---------- | ------ | ------ |
    | 时间复杂度 | O(N)   | O(N)   |
    | 空间复杂度 | O(1)   | O(N)   |

    

    

- 例题2：92 Reverse Linked List 【medium】

- 题意：从m->n的位置翻转链表($1 \leq m \leq n \leq length(list)$ )

- test case:

  > Input:1->2->3->4->5->NULL, m = 2, n = 4
  >
  > Output:1->4->3->2->5->NULL

  

  解题思路：迭代法。

  1、我们定义两个指针，分别称之为g(guard 守卫)和p(point)。
  我们首先根据方法的参数m确定g和p的位置。将g移动到第一个要反转的节点的前面，将p移动到第一个要反转的节点的位置上。我们以m=2，n=4为例。

  ![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200801001040.png)

  2、将p后面的元素删除，然后添加到g的后面。也即头插法。


  3、根据m和n重复步骤（2）
  4、返回dummyHead.next

  ![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200801000946.png)

  

- code：

  ```java
  /*迭代法*/
  class Solution{
         public ListNode reverseBetween(ListNode head, int m, int n) {
          ListNode dummyHead = new ListNode(0);
          dummyHead.next = head;
  
          ListNode g = dummyHead;
          ListNode p = dummyHead.next;
  
          int step = 0;
          while (step < m - 1) {
              g = g.next; p = p.next;
              step ++;
          }
  
          for (int i = 0; i < n - m; i++) {
              ListNode removed = p.next;
              p.next = p.next.next;
  
              removed.next = g.next;
              g.next = removed;
          }
  
          return dummyHead.next;
      }
  
  
  }
  
  /*递归法*/
  class Solution {
      private boolean stop;
      private ListNode left;
      public void recurseAndReverse(ListNode right, int m, int n) {
          if (n == 1) {
              return;
          }
          right = right.next;
  
          if (m > 1) {
              this.left = this.left.next;
          }
  
          this.recurseAndReverse(right, m - 1, n - 1);
  
          if (this.left == right || right.next == this.left) {
              this.stop = true;            
          }
  
          if (!this.stop) {
              int t = this.left.val;
              this.left.val = right.val;
              right.val = t;
              this.left = this.left.next;
          }
      }
  
      public ListNode reverseBetween(ListNode head, int m, int n) {
          this.left = head;
          this.stop = false;
          this.recurseAndReverse(head, m, n);
          return head;
      }
  }
  ```




- 复杂度分析：

  

- | 复杂度     | 迭代法 | 递归法 |
  | ---------- | ------ | ------ |
  | 时间复杂度 | O(N)   | O(N)   |
  | 空间复杂度 | O(1)   | O(N)   |

  迭代法：时间复杂度是O(N), 并且我们是在原链表上进行指针移动的，所以空间复杂度为O(1)

  

  递归法：每个节点最多需遍历两次，一次是常规的递归，一次是回溯的递归，所以时间复杂度是O(N)，在最坏的情况下，我们需要翻转整个链表，并且递归的方法会占用栈，所以空间复杂度是O(N)

  

  这是两个非常典型而且常见的链表翻转类题目，在面试中也经常出现作为热身题，所以需要重点关注。

  > Leetcode中包含翻转链表的题目：	

| 序号 | 题目                                                         | 难度   | 代码 |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| 25   | [Reverse Nodes   in k-Group    ](https://leetcode-cn.com/problems/reverse-nodes-in-k-group) | Hard   | java |
| 61   | [Rotate   List    ](https://leetcode-cn.com/problems/rotate-list) | Medium | java |
| 92   | [Reverse   Linked List II    ](https://leetcode-cn.com/problems/reverse-linked-list-ii) | Medium | java |
| 206  | [Reverse   Linked List    ](https://leetcode-cn.com/problems/reverse-linked-list) | Easy   | java |



### 合并链表

- 例题：21 Merge Two Sorted Lists 【easy】

- 题意：将两个排序好的链表合并成新的有序链表

- test case:

  > Input: 1->2->4, 1->3->4
  >
  > Output: 1->1->2->3->4->4


- 解题思路: **迭代法和递归法**。迭代法是每次比较两个结点，把较小的加到结果链表中，并且这个指针向后移动；递归法即每次比较两个链表的头部，将较小的头部单独取出来，剩下的两个部分继续递归。
- code：

Java

```java
/*迭代法*/
class Solution{
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
		ListNode head = new ListNode(0);
		ListNode cur = head;
		while (l1 != null && l2 != null) {
			if (l1.val >= l2.val) {
				cur.next = l2;
				l2 = l2.next;
			} else {
				cur.next = l1;
				l1 = l1.next;
			}
			cur = cur.next;
		}
 
		if (l1 != null)
			cur.next = l1;
		if (l2 != null)
			cur.next = l2;
		return head.next;
	}
}

/*递归法*/
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val > l2.val) {
            ListNode tmp = l2;
            tmp.next = mergeTwoLists(l1, l2.next);
            return tmp;
        } else {
            ListNode tmp = l1;
            tmp.next = mergeTwoLists(l1.next, l2);
            return tmp;
        }
    }
}
```

- 例题：21 Merge k Sorted Lists (Hard)
- 题意：合并k个有序链表

- 解题思路: 分治算法将链表两两合并，最后合并成一个链表，平均一条链表n个节点，合并两条链表为O(n)，k条链表合并为O(logk)，合并为O(nlogk)

```java
class Solution {
   public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length == 0) return null;
        return partion(lists, 0, lists.length - 1);
    }

    private ListNode partion(ListNode[] lists, int start, int end) {
        if(start == end) {
            return lists[start];
        }
        else if(start < end) {
            int mid = (start + end) / 2;
            ListNode l1 = partion(lists, start, mid);
            ListNode l2 = partion(lists, mid + 1, end);
            return merge(l1, l2);
        }
        else {
            //not gonna happen.
            return null;
        } 
    }

    private ListNode merge(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        if(l1.val < l2.val) {
            l1.next = merge(l1.next, l2);
            return l1;
        } else {
            l2.next = merge(l1, l2.next);
            return l2;
        }
    }
}

```


> LeetCode中包含 合并链表类的题目：

| 序号 | 题目                                                         | 难度   | 代码 |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| 2    | [Add   Two Numbers    ](https://leetcode-cn.com/problems/add-two-numbers) | medium | java |
| 21   | [Merge   Two Sorted Lists    ](https://leetcode-cn.com/problems/merge-two-sorted-lists) | Easy   | java |
| 23   | [Merge   k Sorted Lists    ](https://leetcode-cn.com/problems/merge-k-sorted-lists) | Hard   | java |
| 445  | [Add   Two Numbers II    ](https://leetcode-cn.com/problems/add-two-numbers-ii) | Medium | java |



### 环形链表

- 例题：141 Linked List Cycle 【easy】

- 题意：判断一个单链表是否存在环

- test case:

  > Input : head = [3, 2, 0, -4], pos = 1
  >
  > Output : true
  >
  > why：在这个单链表中存在一个环，尾节点指向第二个节点  

  

- 解题思路：**双指针法**。这道题可以用双指针做，有的也叫快慢指针，或者runner and chaser，意思是从头设置两个指针，一个快指针走2n步（视具体题目而定），慢指针走n步，当快指针走到尾节点时，满指针正好走到链表的一半（视具体题目而定）。在本题中，设置快指针走两步，慢指针一次走一步，如果快指针走到了尽头，则说明链表无环，如果快指针和慢指针相遇就说明链表有环。为什么呢？我们假设一个有环链表，快慢指针最后都会走到环上，而这个环就像一个环形跑道一样，慢指针在后面，快指针在前面，但实际上快指针也在追慢指针，希望能超慢指针一圈。他们在这个跑道上，总会有一天快指针追上了慢指针。我们不用担心快指针跳过了慢指针，因为他们两的速度差是1，所以它们在环上的距离总是每次减1，最后总能减到0。

- code：

Java

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
    if(head==null) return false;
    ListNode slow = head;
    ListNode fast = head;
    while(fast.next!=null && fast.next.next!=null) {
        slow = slow.next;
        fast = fast.next.next;
        if(slow==fast) return true;
    }
    return false;
    }
}
```




- 复杂度分析：时间复杂度O(N)，空间复杂度 O(1)

> LeetCode中含有环形链表的题目：

| 序号 | 题目                                                         | 难度   | 代码 |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| 141  | [Linked   List Cycle    ](https://leetcode-cn.com/problems/linked-list-cycle) | Easy   | java |
| 142  | [Linked   List Cycle II    ](https://leetcode-cn.com/problems/linked-list-cycle-ii) | Medium | java |
| 708  | [Insert   into a Cyclic Sorted List    ](https://leetcode-cn.com/problems/insert-into-a-cyclic-sorted-list) | Medium | java |



### 拆分链表

- 例题：86 Partition List 【medium】

- 题意：给定一个链表以及一个目标值，把小于该目标值的所有节点都移至链表的前端，**大于或等于**目标值的节点移至链表的尾端，**同时要保持这两部分在原先链表中的相对位置。**

- test case:

- 解题思路: **二分法**。设置两个指针left和right，顺序遍历整条链表，left、mid、target三者比较，根据情况left右移或者right左移。关键就在于边界情况和元素有重复。

  - 当 nums[mid] = nums[left] 时，这时由于很难判断 target 会落在哪，那么只能采取 left++

  - 当 nums[mid] > nums[left] 时，这时可以分为两种情况，判断左半部比较简单

  - 当 nums[mid] < nums[left] 时，这时可以分为两种情况，判断右半部比较简单

    

- code：

Java

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = (left + right) / 2;
            if (target == nums[mid]) return true;
            if (nums[mid] == nums[left]) left++;
            
            else if (nums[mid] > nums[left]) {
                if (nums[left] <= target && nums[mid] > target) right = mid - 1;
                else left = mid + 1;
            } else {
                if (nums[mid] < target && target <= nums[right]) left = mid + 1;
                else right = mid - 1;
            }
        }
        return false;
    }
}
```





- 复杂度分析：

> LeetCode中含有拆分类的题目：

| 序号 | 题目                                                         | 难度   | 代码              |
| ---- | ------------------------------------------------------------ | ------ | ----------------- |
| 725  | [Split Linked   List in Parts    ](https://leetcode-cn.com/problems/split-linked-list-in-parts) | Medium | java              |
| ---- | ------------------------------------------------------------ | ------ | ----------------- |
| 86   | [Partition   List    ](https://leetcode-cn.com/problems/partition-list) | Medium | java              |



### 排序链表

- 例题：148 Sort List【medium】
- 题意：在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序
- test case:

>Input: 4->2->1->3
>
>Output: 1->2->3->4

- 解题思路 : **归并排序**。这题有很多解法，题目要有时间复杂度是O(nlogn),满足这个条件的有快速排序，堆排序，归并排序，三者的空间复杂度分别为O(1),O(N),)O(N)。对于链表而言，在进行归并操作时并不需要像数组的归并操作那样分配一个临时数组空间，所以是O(1)的空间复杂度，只需要改变节点的next指针的指向，就可以表示新的归并后的顺序。
- 思考：快排和归并排序的时间复杂度都是O(nlogn)，实践证明快排的速度比归并排序的速度更快，对于数组排序成立，为什么在链表中归并排序更快呢？
- code：

Java

```java
public class Solution {
  
  public ListNode sortList(ListNode head) {
    if (head == null || head.next == null)
      return head;
        
    // step 1.把链表分成两半
    ListNode prev = null, slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }
    
    prev.next = null;
    
    // step 2.对于每一部分的链表进行排序
    ListNode l1 = sortList(head);
    ListNode l2 = sortList(slow);
    
    // step 3. 合并 l2 和 l2
    return merge(l1, l2);
  }
  
  ListNode merge(ListNode l1, ListNode l2) {
    ListNode l = new ListNode(0), p = l;
    
    while (l1 != null && l2 != null) {
      if (l1.val < l2.val) {
        p.next = l1;
        l1 = l1.next;
      } else {
        p.next = l2;
        l2 = l2.next;
      }
      p = p.next;
    }
    
    if (l1 != null)
      p.next = l1;
    
    if (l2 != null)
      p.next = l2;
    
    return l.next;
  }

}
```







- 思考解答：如果待排序的元素存储在数组中，那么快速排序相对归并排序就有两个原因更快。一是，可以很快地进行元素的读取(相对于链表，数组的元素是顺序摆放的，而链表的元素是随机摆放的)，数组的partion这步就比链表的partion这步快。二是，归并排序在merge阶段需要辅助数组，需要申请O(N)的空间，申请空间也是需要时间的。而快排不需要额外申请空间。如果待排序的元素存储在链表中，快排的优点就变成了缺点。归并排序于是就速度更优了。

> LeetCode中 包含链表排序的题目：

| 序号 | 题目                                                         | 难度   | 代码              |
| ---- | ------------------------------------------------------------ | ------ | ----------------- |
| 143  | [Reorder List    ](https://leetcode-cn.com/problems/reorder-list) | Medium | java              |
| ---- | ------------------------------------------------------------ | ------ | ----------------- |
| 147  | [Insertion   Sort List    ](https://leetcode-cn.com/problems/insertion-sort-list) | Medium | java              |
| 148  | [Sort List    ](https://leetcode-cn.com/problems/sort-list)  | Medium | java              |

## 小结

链表的问题是面试当中常常会问到的，比如链表的倒置，删除链表中某个结点，合并两个排序链表，合并 k 个排序链表，排序两个无序链表等。

这些题目一般有一些相应的技巧可以解决。

第一，引入哨兵结点。如我们开头说的  dummy node 结点。在任何时候，不管链表是不是空，head结点都会一直指向这个哨兵结点。我们也把这种有哨兵结点的链表叫做带头链表。<br/>

第二，双指针法。这种用法适用于查找链表中某个位置，判断链表是否有环等<br/>

第三，分之归并法。这种用法适用于链表的排序处理，如合并 k 个排序链表，排序两个无序链表等。<br/>

第四，在解答的过程中，要多考虑边界情况。
  - 链表为空
  - 链表中只有一个结点
  - 链表中只包含两个结点
  - 代码在处理头结点跟尾结点是否存在什么问题




参考资料：

1.https://leetcode-cn.com/problems/sort-list/discuss/46714/Java-merge-sort-solution

2.https://leetcode-cn.com/problems/merge-two-sorted-lists/discuss/9735/Python-solutions-(iteratively-recursively-iteratively-in-place).




## **往期文章**

[Android 面试必备 - http 与 https 协议](https://blog.csdn.net/gdutxiaoxu/article/details/97885526)

[Android 面试必备 - 计算机网络基本知识（TCP，UDP，Http，https）](https://blog.csdn.net/gdutxiaoxu/article/details/97618598)

[Android 面试必备 - 线程](https://blog.csdn.net/gdutxiaoxu/article/details/98475465)

[Android 面试必备 - JVM 及 类加载机制](https://xujun.blog.csdn.net/article/details/98896053)

[Android 面试必备 - 系统、App、Activity 启动过程](https://xujun.blog.csdn.net/article/details/99006458)

[面试官系列- 你真的了解 http 吗](https://blog.csdn.net/gdutxiaoxu/article/details/107349652)

[面试官问， https 真的安全吗，可以抓包吗，如何防止抓包吗](https://xujun.blog.csdn.net/article/details/107393249)

[java 版剑指offer算法集锦](https://juejin.im/post/6854573217038909454)

**[Android_interview github 地址](https://github.com/gdutxiaoxu/Android_interview)**   帮忙 star



**如果你觉得对你有所帮助的话，可以关注我的公众号 徐公码字（stormjun94)，第一时间会在上面更新**



![](https://raw.githubusercontent.com/gdutxiaoxu/blog_pic/master/offer/20200722234908.png)



