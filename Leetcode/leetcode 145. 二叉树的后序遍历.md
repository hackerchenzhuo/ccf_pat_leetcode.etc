# 原创：leetcode 145. 二叉树的后序遍历

**后序：（前-&gt;后-&gt;中） 其实就是 （中-&gt;后-&gt;前）的逆序————吧前序的前 后 调换，然后reverse就行。**

**代价就是速度减慢：**

执行用时 : 8 ms, 在Binary Tree Postorder Traversal的C++提交中击败了85.75% 的用户

内存消耗 : 9.3 MB, 在Binary Tree Postorder Traversal的C++提交中击败了25.52% 的用户

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
    vector<int> postorderTraversal(TreeNode* root) {
         //中前后
        //非递归：栈
        stack<TreeNode*>sta;
        vector<int> ans;
        while(root!=NULL||!sta.empty())
        {
            
            while(root!=NULL)
            {
                ans.push_back(root->val);
                sta.push(root);
                root=root->right;
            }
            if(!sta.empty())
            {
                root=sta.top();
                sta.pop();            
                root=root->left;
            }
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
``` 

 
