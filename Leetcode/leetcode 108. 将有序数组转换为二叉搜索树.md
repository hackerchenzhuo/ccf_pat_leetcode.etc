# 原创：leetcode 108. 将有序数组转换为二叉搜索树

 在递归函数中建立新树。一次建立一棵树，而不是两棵。

 
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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return func(nums,0,nums.size()-1);
    }
    TreeNode* func(vector<int>& nums,int l,int r){
        if(r<l) return NULL;
        int mid = l+((r-l)>>1);
        TreeNode* root=new TreeNode(nums[mid]);
        root->left=func(nums,l,mid-1);
        root->right=func(nums,mid+1,r);
        return root;
    }
};
```