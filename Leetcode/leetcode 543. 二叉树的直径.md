# 原创：leetcode 543. 二叉树的直径

方法一：（无脑DFS）n 次递归（n是深度）

注意。不一定最大宽度每次都经过根节点

执行用时 : 108 ms, 在Diameter of Binary Tree的C++提交中击败了5.26% 的用户

内存消耗 : 35.8 MB, 在Diameter of Binary Tree的C++提交中击败了5.39%的用户
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
    int diameterOfBinaryTree(TreeNode* root) {
        if(root==NULL) return 0;
        int t=dfs(root->left)+dfs(root->right);
        int ans=max(diameterOfBinaryTree(root->right),diameterOfBinaryTree(root->left));
        return max(t,ans);
    }
    int dfs(TreeNode* root)
    {
        if(root==NULL) return 0;
        return 1+max(dfs(root->left),dfs(root->right));
    }
};
```
剪枝：节约一半的时间（不用每次遍历到最后）

执行用时 : 56 ms, 在Diameter of Binary Tree的C++提交中击败了13.36% 的用户

内存消耗 : 36.2 MB, 在Diameter of Binary Tree的C++提交中击败了5.39%的用户
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
    int diameterOfBinaryTree(TreeNode* root,int last=0) {
        if(root==NULL) return 0;
        int t1=dfs(root->left),t2=dfs(root->right);
        if(max(t1,t2)<0.5*last) return 0;
        int t=t1+t2;
        int ans=max(diameterOfBinaryTree(root->right,t),diameterOfBinaryTree(root->left,t));
        return max(t,ans);
    }
    int dfs(TreeNode* root)
    {
        if(root==NULL) return 0;
        return 1+max(dfs(root->left),dfs(root->right));
    }
};
```
 

更加好的：（一次递归）

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
    int mx=0;
    int diameterOfBinaryTree(TreeNode* root) {
        depth(root);
        return mx;
    }
    int depth(TreeNode* root)
    {
        if(root==nullptr)return 0;
        int left=depth(root->left);
        int right=depth(root->right);
        mx=max(left+right,mx);
        return max(left,right)+1;
        
    }
};
``` 
