# 原创：leetcode 107. 二叉树的层次遍历 II【队列】

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        int num=1;
        vector<vector<int>> ans;
        queue<TreeNode*> s;
        if(!root)   return ans;
        s.push(root);
        TreeNode*t;
        int k=1;
        while(!s.empty())
        {
            num=k;
            k=0;
            vector<int> v;
            while(num--)
            {
            t=s.front();s.pop();v.push_back(t->val);
            if(t->left!=NULL) {
                s.push(t->left);k++;
            }
            if(t->right!=NULL) {
                s.push(t->right);k++;
            }
            }
            ans.push_back(v);
        }
        reverse(ans.begin(),ans.end());
        return ans;
        
    }
};
``` 
