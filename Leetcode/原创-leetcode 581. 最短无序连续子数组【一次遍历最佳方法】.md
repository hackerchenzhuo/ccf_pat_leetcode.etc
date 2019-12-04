# 原创：leetcode 581. 最短无序连续子数组【一次遍历最佳方法】

方法一、先sort再比对。

执行用时 : 80 ms, 在Shortest Unsorted Continuous Subarray的C++提交中击败了34.15% 的用户

内存消耗 : 11.4 MB, 在Shortest Unsorted Continuous Subarray的C++提交中击败了69.79% 的用户

方法二、

一次遍历

【找到**从前往后**最后一个比前半部分**当前最大值**小的】

【找到**从后往前**最后一个比后半部分**当前最小值**大的】

执行用时 : 36 ms, 在Shortest Unsorted Continuous Subarray的C++提交中击败了97.79% 的用户

内存消耗 : 10.4 MB, 在Shortest Unsorted Continuous Subarray的C++提交中击败了91.37% 的用户

 
