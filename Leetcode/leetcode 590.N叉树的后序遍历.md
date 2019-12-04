# 原创：leetcode 590.N叉树的后序遍历

 

方法一：【比较慢。用的递归思想】

**执行用时 : 288 ms, 在N-ary Tree Postorder Traversal的C++提交中击败了62.39% 的用户**

**内存消耗 : 127.3 MB, 在N-ary Tree Postorder Traversal的C++提交中击败了10.94% 的用户**

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;
    Node() {}
    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    vector<int> ans;
    vector<int> postorder(Node* root) {
        if(root==NULL) return {};
        for(int i=0;i<root->children.size();i++)
        {
            postorder(root->children[i]);
        }
        ans.push_back(root->val);
        return ans;
    }
};
```

方法二：栈的实现
```c++
#define par pair<Node*,int> // 0: travel 1: output
class Solution {
public:
    vector<int> postorder(Node* root) {
        vector<int> ret;
        if(!root) return ret;        
        stack<par> s;
        s.push(par(root,0));
        while(!s.empty()){
            par cur = s.top();s.pop();
            if(cur.second==1){
                ret.push_back(cur.first->val);
                continue;
            }
            s.push(par(cur.first,1));
            for(int i = cur.first->children.size()-1;i>=0;--i){
                s.push(par(cur.first->children[i],0));
            }
        }
        return ret;        
    }
};
```
 
