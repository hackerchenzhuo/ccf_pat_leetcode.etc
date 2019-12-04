# 原创：leetcode 110. 平衡二叉树

无脑写法：双重递归——一个找深度，一个判平衡：

没有重复利用深度，深度进行了重复测量，浪费了时间：

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
    bool isBalanced(TreeNode* root) {
        if(root==NULL) return true;
        if(abs(find(root->left)-find(root->right))>1) return false;
        else return isBalanced(root->left)&&isBalanced(root->right);
    }
    
    int find(TreeNode* root)//找最大深度
    {
        if(root==NULL) return 0;
        else return 1+max(find(root->left),find(root->right));
    }
};
```

 不重复计算：加入flag标志位，在寻找深度的过程中进行比较，一旦出现不平衡状态则退出。时间快一倍

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
    int flag=0;
    bool isBalanced(TreeNode* root) {
        find(root);
        if(flag) return false;
        return true;
    }
    
    int find(TreeNode* root)//找最大深度
    {
        if(root==NULL) return 0;
        int l=find(root->left);
        int r=find(root->right);
        if(abs(l-r)>1){
            flag=1;return 1;
        }
        else return 1+max(l,r);
    }
};
```

 

 

 
