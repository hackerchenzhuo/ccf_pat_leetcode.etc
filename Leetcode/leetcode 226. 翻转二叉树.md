# 原创：leetcode 226. 翻转二叉树

递归求解：

执行用时 : 4 ms, 在Invert Binary Tree的C++提交中击败了96.52% 的用户

内存消耗 : 9.4 MB, 在Invert Binary Tree的C++提交中击败了5.20% 的用户

我的方法：
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        rev(root);
        return root;
    }
    void rev(TreeNode* t)
    {
        
        if(t!=NULL&&!(t->left==NULL&&t->right==NULL))//如果不是都为空
        {
            TreeNode* tmp=NULL;
            tmp=t->left;
            t->left=t->right;
            t->right=tmp;
            rev(t->left);
            rev(t->right);
        }
    }
};
```
 

 最简单方法：

执行用时 : 4 ms, 在Invert Binary Tree的C++提交中击败了96.52% 的用户

内存消耗 : 9.1 MB, 在Invert Binary Tree的C++提交中击败了43.78% 的用户
```c++
   TreeNode* invertTree(TreeNode* root) {
	    if(root==NULL)
			return NULL;
		TreeNode * ptmpNode = root->left;
		root->left = invertTree(root->right);
		root->right = invertTree(ptmpNode);
		return root;
    }
```
 
