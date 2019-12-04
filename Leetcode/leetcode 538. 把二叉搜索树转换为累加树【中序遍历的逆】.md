# 原创：leetcode 538. 把二叉搜索树转换为累加树【中序遍历的逆】

 

常规：

两次中序遍历。

执行用时 : 88 ms, 在Convert BST to Greater Tree的C++提交中击败了39.07% 的用户

内存消耗 : 24 MB, 在Convert BST to Greater Tree的C++提交中击败了79.60% 的用户
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
    vector<int> num;
    int j;
    TreeNode* convertBST(TreeNode* root) {
        //两次中序遍历进行修改；
        //第一次中序遍历，存入数组
        midsrh(root);
        //数组从后往前累加
        int sz=num.size();
        int t=0;
        for(int i=sz-1;i>=0;i--)
        {    
            num[i]+=t;
            t=num[i];
        }
        //再一次中序遍历，修改二叉树
        j=0;
        midsrh2(root);
        return root;
    }
    void midsrh(TreeNode* root)
    {
        if(root==NULL)
            return;
        midsrh(root->left);
        num.push_back(root->val);
        midsrh(root->right);
        
    }
    void midsrh2(TreeNode* root)
    {
        if(root==NULL)
            return;
        midsrh2(root->left);
        root->val=num[j];
        j++;
        midsrh2(root->right);
        
    }
};
```
 

改进：

一次中序遍历的逆过程：

 

**执行用时 : 44 ms, 在Convert BST to Greater Tree的C++提交中击败了97.88% 的用户**

**内存消耗 : 23.5 MB, 在Convert BST to Greater Tree的C++提交中击败了85.57% 的用户**

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
    int t;
    TreeNode* convertBST(TreeNode* root) {
        t=0;
        midsrh(root);
        return root;
    }
    void midsrh(TreeNode* root)
    {
        if(root==NULL)
            return;
        midsrh(root->right);
        root->val+=t;
        t=root->val;
        midsrh(root->left);
        
    }
 
};
``` 
