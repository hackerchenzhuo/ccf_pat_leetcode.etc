# 原创：leetcode 114. 二叉树展开为链表【前序遍历】

**中文版**

执行用时 :12 ms, 在所有C++提交中击败了88.57%的用户

内存消耗 :10.1 MB, 在所有C++提交中击败了71.67%的用户

**英文版**

Runtime: 8 ms, faster than 85.11% of C++ online submissions for Flatten Binary Tree to Linked List.

Memory Usage: 10.4 MB, less than 40.69% of C++ online submissions for Flatten Binary Tree to Linked List.

### 给定一个二叉树，原地将它展开为链表。

> 
例如，给定二叉树
<p>    1<br/>
   / \<br/>
  2   5<br/>
 / \   \<br/>
3   4   6<br/>
将其展开为：</p>
<p>1<br/>
 \<br/>
  2<br/>
   \<br/>
    3<br/>
     \<br/>
      4<br/>
       \<br/>
        5<br/>
         \<br/>
          6</p>
 


**用的比较笨的方法。但其实也挺奏效**

（1）先前序遍历，并且按顺序存入vector数组

（2）按vector数组的顺序依次给root接上尾巴~（记得要把左孩子置空）

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
    vector<TreeNode*>ans;
    void flatten(TreeNode* root) {
        //前序遍历：
        if(root==NULL) return;
        preorder(root);
        int i=1;
        TreeNode* t=root;
        while(i<ans.size())
        {
            t->right=ans[i];
            t->left=NULL;
            t=t->right;
            i++;
        }
        //到最后一个结点的时候肯定没用孩子了，因为是前序遍历。
    }
    void preorder(TreeNode* root)
    {
        if(root==NULL) return;
        ans.push_back(root);
        preorder(root->left);
        preorder(root->right);
    }
};
``` 
