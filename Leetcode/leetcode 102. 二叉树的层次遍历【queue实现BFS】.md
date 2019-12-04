# 原创：leetcode 102. 二叉树的层次遍历【queue实现BFS】

> 
**执行用时 :4 ms, 在所有C++提交中击败了99.43%的用户**
**内存消耗 :13.9 MB, 在所有C++提交中击败了45.55%的用户**


关键：

> 
<p>        vector&lt;vector&lt;int&gt;&gt; ans;<br/>
        vector&lt;int&gt; tmp;</p>
        int left=1,next=0; 


> 
**ans：答案**
**tmp：存一层的结点**
**left：这层还剩多少结点**
**tmp：下一层有多少结点 **


 

## 方法二：

不需要next和left来存长度。可以直接在一层结点的left和right入队后统计队列长度，然后改长度就是下一层次的结点数。

 

## 其他捷径方法：

### DFS递归算法

最简单的解法就是递归，首先确认树非空，然后调用递归函数 helper(node, level)，参数是当前节点和节点的层次。程序过程如下：

输出列表称为 levels，当前最高层数就是列表的长度 len(levels)。比较访问节点所在的层次 level 和当前最高层次 len(levels) 的大小，如果前者更大就向 levels 添加一个空列表。<br/>
将当前节点插入到对应层的列表 levels[level] 中。<br/>
递归非空的孩子节点：helper(node.left / node.right, level + 1)。

**这种方法不是纯粹的层次遍历，只是这个题刚好很适合这种方法。如果是单纯层次遍历按顺序输出的话这样做会产生很高的空间复杂度**

 
