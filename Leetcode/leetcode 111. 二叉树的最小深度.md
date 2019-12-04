# 原创：leetcode 111. 二叉树的最小深度

记住：最小深度和最大深度方法不同。最小深度要小心非叶子结点的干扰。 

**执行用时 : 28 ms, 在Minimum Depth of Binary Tree的C++提交中击败了95.85% 的用户**

**内存消耗 : 20.1 MB, 在Minimum Depth of Binary Tree的C++提交中击败了7.68% 的用户**
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
    int minDepth(TreeNode* root) {
        if(root==NULL) return 0;
        else if(root->left&&!root->right) return 1+minDepth(root->left);
        else if(!root->left&&root->right) return 1+minDepth(root->right);
        else return 1+min(minDepth(root->left),minDepth(root->right));
    }
 
 
};
```

 
