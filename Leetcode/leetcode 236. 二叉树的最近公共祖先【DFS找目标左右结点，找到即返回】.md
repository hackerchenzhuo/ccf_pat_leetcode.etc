# 原创：236. 二叉树的最近公共祖先【DFS找目标左右结点，找到即返回】

方法一：

**执行用时 :60 ms, 在所有C++提交中击败了10.44%的用户**

**内存消耗 :33.9 MB, 在所有C++提交中击败了5.06%的用户**

这map是有多慢。。  
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
    //注意：一个节点也可以是它自己的祖先
    //可以认为没有相同的元素。
    map<TreeNode*,TreeNode*> father;//存父节点
    map<TreeNode*,int> ans;//存遍历的路径
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        //深度遍历
        //用字典存相遇结点
        //1.先dfs遍历
        if(root==NULL) return NULL;
        dfs(root);
        //2.找相遇结点,先把p的路径全部绘制出来
        while(father[p])
        {
            ans[p]=1;
            p=father[p];
        }
        while(father[q])
        {
            if(ans[q]==1)
            {
                return q;
            }
            q=father[q];
        }
        return root;//到这里只可能是root了
    }
    void dfs(TreeNode* root)
    {
        if(root->left!=NULL)
        {
            father[root->left]=root;
            dfs(root->left);
        }
        if(root->right!=NULL)
        {
            father[root->right]=root;
            dfs(root->right);
        }
    }
};
```
别人家优秀的答案：就是我最开始的想法：DFS

【转】

> 
<p>做了一些二叉树的题，发现二叉树的查找问题一般都是从左右子树递归去解决，也往往都能得到答案，因此，这道题可以考虑是否能从左右子树进行递归去解决呢？<br/>
首先，要想通过递归来实现，就需要先确定临界条件，那么临界条件是什么呢？换句话说，临界条件就是递归中能够直接返回的特殊情况，第一点则是最常见的“判空”，判断根结点是否是空节点，如果是，那么肯定就可以马上返回了，这是一个临界条件；再来考虑题意，在以root为根结点的树中找到p结点和q结点的最近公共祖先，那么特殊情况是什么呢？很显然，特殊情况就是根结点就等于q结点或p结点的情况，想一下，如果根结点为二者之一，那么根结点就必定是最近公共祖先了，这时直接返回root即可。由此看来，这道题就一共有三种特殊情况，root == q 、root == p和root==null，这三种情况均直接返回root即可。<br/>
根据临界条件，实际上可以发现这道题已经被简化为查找以root为根结点的树上是否有p结点或者q结点，如果有就返回p结点或q结点，否则返回null。<br/>
这样一来其实就很简单了，从左右子树分别进行递归，即查找左右子树上是否有p结点或者q结点，就一共有4种情况：<br/>
第一种情况：左子树和右子树均找没有p结点或者q结点；（这里特别需要注意，虽然题目上说了p结点和q结点必定都存在，但是递归的时候必须把所有情况都考虑进去，因为题目给的条件是针对于整棵树，而递归会到局部，不一定都满足整体条件）<br/>
第二种情况：左子树上能找到，但是右子树上找不到，此时就应当直接返回左子树的查找结果；<br/>
第三种情况：右子树上能找到，但是左子树上找不到，此时就应当直接返回右子树的查找结果；<br/>
第四种情况：左右子树上均能找到，说明此时的p结点和q结点分居root结点两侧，此时就应当直接返回root结点了。<br/>
综上也不难写出结果了：<br/>
 </p>

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==p||root==q||!root)return root;//特殊情况1+2
        
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        
        if (left && right) return root;//找到了。直接返回
        if (left) return left;
        if (right) return right;
        return NULL;
    }
};
```
 
