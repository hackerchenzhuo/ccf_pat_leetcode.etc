# 原创：leetcode 543. 二叉树的直径

方法一：（无脑DFS）n 次递归（n是深度）

注意。不一定最大宽度每次都经过根节点

执行用时 : 108 ms, 在Diameter of Binary Tree的C++提交中击败了5.26% 的用户

内存消耗 : 35.8 MB, 在Diameter of Binary Tree的C++提交中击败了5.39%的用户

剪枝：节约一半的时间（不用每次遍历到最后）

执行用时 : 56 ms, 在Diameter of Binary Tree的C++提交中击败了13.36% 的用户

内存消耗 : 36.2 MB, 在Diameter of Binary Tree的C++提交中击败了5.39%的用户

 

更加好的：（一次递归）

 
