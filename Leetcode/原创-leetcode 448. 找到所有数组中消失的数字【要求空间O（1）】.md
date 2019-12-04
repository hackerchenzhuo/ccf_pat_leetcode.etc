# 原创：leetcode 448. 找到所有数组中消失的数字【要求空间O（1）】

方法一：

空间换时间（easy）

执行用时 : 132 ms, 在Find All Numbers Disappeared in an Array的C++提交中击败了96.39% 的用户

内存消耗 : 16.1 MB, 在Find All Numbers Disappeared in an Array的C++提交中击败了6.77% 的用户

方法二：

空间复杂度O（1）：

**将所有正数作为数组下标，置对应数组值为负值。那么，仍为正数的位置即为（未出现过）消失的数字。**

执行用时 : 140 ms, 在Find All Numbers Disappeared in an Array的C++提交中击败了94.98% 的用户

内存消耗 : 14.8 MB, 在Find All Numbers Disappeared in an Array的C++提交中击败了86.06% 的用户

 
