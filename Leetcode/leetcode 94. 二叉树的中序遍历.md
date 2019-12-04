# 原创：leetcode 94. 二叉树的中序遍历

执行用时 : 0 ms, 在Binary Tree Inorder Traversal的C++提交中击败了100.00% 的用户

内存消耗 : 10.8 MB, 在Binary Tree Inorder Traversal的C++提交中击败了8.14% 的用户

**给定一个二叉树，返回它的中序 遍历。**

> 
示例:
<p>输入: [1,null,2,3]<br/>
   1<br/>
    \<br/>
     2<br/>
    /<br/>
   3</p>
<p>输出: [1,3,2]<br/>
进阶: 递归算法很简单，你可以通过**迭代算法**完成吗？</p>


来源：力扣（LeetCode）<br/>
链接：https://leetcode-cn.com/problems/binary-tree-inorder-traversal<br/>
递归解法：
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
    vector<int> ans;
    vector<int> inorderTraversal(TreeNode* root) {
        //前中后
        if(root==NULL) return {};
        inorderTraversal(root->left);
        ans.push_back(root->val);
        inorderTraversal(root->right);
        return ans;
    }
    
};
```
 

非递归：【使用栈】

执行用时 : 4 ms, 在Binary Tree Inorder Traversal的C++提交中击败了96.24%的用户

内存消耗 : 9.3 MB, 在Binary Tree Inorder Traversal的C++提交中击败了34.53% 的用户

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
 
    vector<int> inorderTraversal(TreeNode* root) {
        //非递归：栈
        stack<TreeNode*>sta;
        vector<int> ans;
        while(root!=NULL||!sta.empty())
        {
            while(root!=NULL)
            {
                sta.push(root);
                root=root->left;
            }
            if(!sta.empty())
            {
                root=sta.top();
                sta.pop();
                ans.push_back(root->val);
                root=root->right;
            }
        }
        return ans;
    }
    
};
``` 
