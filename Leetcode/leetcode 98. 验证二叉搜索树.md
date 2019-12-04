# 原创：leetcode 98. 验证二叉搜索树

**给定一个二叉树，判断其是否是一个有效的二叉搜索树。**

假设一个二叉搜索树具有如下特征：

> 
<p>节点的左子树只包含小于当前节点的数。<br/>
节点的右子树只包含大于当前节点的数。<br/>
所有左子树和右子树自身必须也是二叉搜索树。<br/>
示例 1:</p>
<p>输入:<br/>
    2<br/>
   / \<br/>
  1   3<br/>
输出: true<br/>
示例 2:</p>
<p>输入:<br/>
    5<br/>
   / \<br/>
  1   4<br/>
     / \<br/>
    3   6<br/>
输出: false<br/>
解释: 输入为: [5,1,4,null,null,3,6]。<br/>
     根节点的值为 5 ，但是其右子节点值为 4 。</p>


执行用时 : 20 ms, 在Validate Binary Search Tree的C++提交中击败了92.44%的用户

内存消耗 : 21 MB, 在Validate Binary Search Tree的C++提交中击败了11.42%的用户

> 
**很容易想到这一点：**
**中序遍历，然后判断是否有序。**
**如果有序就是二叉搜索树。**

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
    bool isValidBST(TreeNode* root) {
        //先中序遍历
        //然后判断是否有序
        if(root==NULL) return true;
        bsort(root);
        int i=1,j=0;
        while(i!=ans.size())
        {
            if(ans[i]<=ans[j]) return false;
            i++;j++;
        }
        return true;
        
    }
    void bsort(TreeNode* root)
    {
        if(root==NULL) return;
        bsort(root->left);
        ans.push_back(root->val);
        bsort(root->right);
    }
};
```

 

 但是这个方法肯定不是最佳的。

# 最佳方法：

在中序遍历的同时进行比较，这样就不需要二次遍历了。

**执行用时 : 16 ms, 在Validate Binary Search Tree的C++提交中击败了96.63%的用户**

**内存消耗 : 21.2 MB, 在Validate Binary Search Tree的C++提交中击败了5.16% 的用户**

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
    int flag=0;
    bool isValidBST(TreeNode* root) {
        //先中序遍历
        //然后判断是否有序
        if(root==NULL) return true;
        bsort(root);
        if(flag) return false;
        return true;
        
    }
    void bsort(TreeNode* root)
    {
        if(flag||root==NULL) return ;//结束搜索
        bsort(root->left);
        ans.push_back(root->val);
        int res;
        if(!flag&&ans.size()>1&&ans[ans.size()-1]<=ans[ans.size()-2])
            //还没找到
            //ans数组有至少2个元素且当前最后一个大于前一个
        {
            flag=1;return;
        }
        bsort(root->right);
        
    }
};
``` 
