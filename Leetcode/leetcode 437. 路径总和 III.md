# 原创：leetcode 437. 路径总和 III

 

借用的他人的代码：不要想得过于复杂。把中间步骤分解，easy的。

两种情况：

> 
1.包括当前结点
2.不包括当前结点


然后dfs一下。

 

执行用时 : 28 ms, 在Path Sum III的C++提交中击败了96.77% 的用户

内存消耗 : 14.6 MB, 在Path Sum III的C++提交中击败了80.08% 的用户

```c++
class Solution {
public:
    int dfs(TreeNode* T, int sum)
    {//深度优先遍历，搜索某子树的所有可能路径
        int res = 0;
        if(T == NULL)
            return res;//节点为空时返回0
        if(sum == T->val)
            res++;//此时说明到该节点的路径是符合要求的
        res += dfs(T->left, sum - T->val);//目前的路径数目+遍历左子树得到的路径数目；
        res += dfs(T->right, sum - T->val);
        return res;
    }
 
    int pathSum(TreeNode* root, int sum) {
        if(NULL == root)
            return 0;
        return dfs(root, sum) + pathSum(root->left, sum) + pathSum(root->right, sum);
    }//每次递归做三件事：搜索节点T开始的子树的所有路径、递归到左子树重复、递归到右子树重复
};
``` 
