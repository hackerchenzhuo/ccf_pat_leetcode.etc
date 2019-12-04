# 原创：leetcode 617.合并二叉树【递归连接二叉树】

执行用时 : 40 ms, 在Merge Two Binary Trees的C++提交中击败了99.62% 的用户

内存消耗 : 13.8 MB, 在Merge Two Binary Trees的C++提交中击败了84.32%的用户

 

递归使用二叉树，进行连接。千万不要使用new！！！！

千万不要单独或者多余地判断！！！

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
    //二叉树的连接：使用返回值
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if(t1==NULL&&t2==NULL) return NULL;
        else if(t1==NULL&&t2!=NULL) {
            t1=t2;//连接
            return t1;
        }
        else if(t1!=NULL&&t2==NULL)
        {
            return t1;
        }
        else 
        {
            t1->val=t1->val+t2->val;
            
        }
        t1->left=mergeTrees(t1->left, t2->left);
        t1->right=mergeTrees(t1->right, t2->right);  
        return t1;
    }
};
``` 
