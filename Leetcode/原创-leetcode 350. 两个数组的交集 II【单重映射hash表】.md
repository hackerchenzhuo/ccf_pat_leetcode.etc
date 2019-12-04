# 原创：leetcode 350. 两个数组的交集 II【单重映射hash表】

 

**执行用时 : 20 ms, 在Intersection of Two Arrays II的C++提交中击败了50.66% 的用户**

**内存消耗 : 10.8 MB, 在Intersection of Two Arrays II的C++提交中击败了5.03% 的用户**

方法一：使用hash的map表映射。时间复杂度：O（n）。类似于三次遍历。

使用map&lt;int,vector&lt;int&gt;&gt; 的数据结构。有点麻烦

## **其实可以用单重hash 表-&gt;两次遍历**

 

 单重映射：

**执行用时 : 16 ms, 在Intersection of Two Arrays II的C++提交中击败了81.92% 的用户**

**内存消耗 : 9.9 MB, 在Intersection of Two Arrays II的C++提交中击败了5.03%的用户**

 
