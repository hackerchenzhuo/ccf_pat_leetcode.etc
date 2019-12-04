# 原创：leetcode 105. 从前序与中序遍历序列构造二叉树【递归构造二叉树，以下标为传递对象】c++

**执行用时 :20 ms, 在所有C++提交中击败了99.54%的用户**

**内存消耗 :16.4 MB, 在所有C++提交中击败了91.80%的用户**

> 
根据一棵树的前序遍历与中序遍历构造二叉树。
<p>注意:<br/>
你可以**假设树中没有重复的元素。**</p>
例如，给出
<p>前序遍历 preorder = [3,9,20,15,7]<br/>
中序遍历 inorder = [9,3,15,20,7]<br/>
返回如下的二叉树：</p>
<p>    3<br/>
   / \<br/>
  9  20<br/>
    /  \<br/>
   15   7</p>
 


递归构造二叉树

为了减少参数的传递，尽量避免多余参数的定义（虽然这样子会显得很杂乱）。。。

参数如下：

> 
int pre1：前序遍历数列中的起点
int pre2：前序遍历数列中的终点
int in1：中序遍历数列中的起点
int in2：中序遍历数列中的终点

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        //递归迭代
        //前序：中前后
        //中序：前中后
        //可以假设树中没有重复的元素。
        if(preorder.size()==0) return NULL;
        return getroot(preorder,inorder,0,preorder.size()-1,0,inorder.size()-1);
    }
    TreeNode* getroot(vector<int>& preorder,vector<int>& inorder,int pre1,int pre2,int in1,int in2)
    {
        if(pre2-pre1<0||in2-in1<0) return NULL;
        TreeNode* root=new TreeNode(preorder[pre1]);//前序段的第一个
        int indx=in1;//中序中根的下标
        for( ;indx<inorder.size();indx++)
        {
            if(inorder[indx]==preorder[pre1])
                break;
        }
        
        root->left=getroot(preorder,inorder,pre1+1,pre1+indx-in1,in1,indx-1);
        root->right=getroot(preorder,inorder,pre1+indx-in1+1,pre2,indx+1,in2);
        return root;
        
    }
    
};
```
 
