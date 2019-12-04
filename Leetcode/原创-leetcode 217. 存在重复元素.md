# 原创：leetcode 217. 存在重复元素

方法一：hash表（两遍遍历）

O（2n）

执行用时 : 120 ms, 在Contains Duplicate的C++提交中击败了14.24% 的用户

内存消耗 : 18.2 MB, 在Contains Duplicate的C++提交中击败了5.09% 的用户

 

方法二：hash表（一遍遍历！！！！！！！！！！！！！）

时间复杂度O（n/2）

**执行用时 : 68 ms, 在Contains Duplicate的C++提交中击败了50.80% 的用户**

**内存消耗 : 16.6 MB, 在Contains Duplicate的C++提交中击败了21.51% 的用户**

 

方法三：

先排序再看相邻的有没有相同：O（nlogn） 我觉得没啥用。。

试了一下，惊呆了

执行用时 : 56 ms, 在Contains Duplicate的C++提交中击败了74.35% 的用户

内存消耗 : 11.4 MB, 在Contains Duplicate的C++提交中击败了61.46% 的用户

不科学啊

还有一种比较妙的方法：

利用set不存重复的原则。

 
