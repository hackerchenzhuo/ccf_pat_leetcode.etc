# 原创：leetcode 144. 二叉树的前序遍历【非递归，在中序的基础上修改一丢丢】

执行用时 : 4 ms, 在Binary Tree Inorder Traversal的C++提交中击败了96.24%的用户

内存消耗 : 9.3 MB, 在Binary Tree Inorder Traversal的C++提交中击败了34.53% 的用户

 

**在进栈前入队，实现前序。（中-&gt;前-&gt;后）**

**出栈时入队，实现中序。（前-&gt;中-&gt;后）**

**后序：（前-&gt;后-&gt;中） 其实就是 （中-&gt;后-&gt;前）的逆序————吧前序的前 后 调换，然后reverse就行。**
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
    vector<int> preorderTraversal(TreeNode* root) {
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
                root=root->left;
            }
            if(!sta.empty())
            {
                root=sta.top();
                sta.pop();            
                root=root->right;
            }
        }
        return ans;
    }
};
```

 
