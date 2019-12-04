# 原创：leetcode 101. 对称二叉树【递归】

 
```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        return same(root->left,root->right);
    }
    
    bool same(TreeNode*l,TreeNode*r)
    {
        if(!l&&!r) return true;
        if(!l&&r|| l&&!r || l->val!=r->val) return false;
        return(same(l->left,r->right)&&same(l->right,r->left));
    }
};
```