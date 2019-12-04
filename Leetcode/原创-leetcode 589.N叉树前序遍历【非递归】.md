# 原创：leetcode 589.N叉树前序遍历【非递归】

执行用时 : 288 ms, 在N-ary Tree Postorder Traversal的C++提交中击败了62.39% 的用户

内存消耗 : 127.3 MB, 在N-ary Tree Postorder Traversal的C++提交中击败了10.94% 的用户

 

利用栈的思想，从后往前入栈，后入先出。

在出栈的时候统一push_back（OR直接print）到ans数组中。

实现前序遍历的序列输出

 
