# 原创：leetcode 429. N叉树的层序遍历【层次遍历用 队列queue+BFS 】

**Runtime: 148 ms, faster than 92.87% of C++ online submissions for N-ary Tree Level Order Traversal.**

**Memory Usage: 34 MB, less than 41.25% of C++ online submissions for N-ary Tree Level Order Traversal.**

 

简单的BFS（花了我30分钟，吐血了）

**队列**读入然后输出。

注意：

由于输出是按层输出，所以需要保留**当层次剩余的结点数量**以及**下一层次有多少结点。**

> 
** int left=1,next=0;//left：该层剩余多少；next：下一层有多少**

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
    //层次遍历用BFS 队列
    
    vector<vector<int> > ans;
    vector<int> tmp;
    vector<vector<int>> levelOrder(Node* root) {
        if(root==NULL) return {};
        queue<Node*> q;
        q.push(root);
        int left=1,next=0;//left：该层剩余多少；next：下一层有多少
        while(!q.empty())//q不为空
        {
            root=q.front();
            q.pop();
            left--;
            tmp.push_back(root->val);
            for(int i=0;i<root->children.size();i++)
            {
                next++;
                q.push(root->children[i]);
            }
            
            if(left==0) //这一层遍历结束了
            {
                cout<<"1"<<endl;
                ans.push_back(tmp);
                tmp.clear();
                left=next;
                next=0;
            }
            
        }
        return ans;
    }
    
};
```
 

方法二：DFS

这个层次遍历有点特别，因为他输出**并不是按层次遍历的顺序输出，而是放到数组里**。

这样以来可以用DFS的方法解决。【**这也为按顺序输出的层次遍历提供了一种思路**】

：

若当前的层次level 大于ans 的size

则给 ans 添加一层vector，然后在ans[level]中push_back当前的元素。

这样做起来也挺简单。时间上差不多

 

**Runtime: 144 ms, faster than 97.35% of C++ online submissions for N-ary Tree Level Order Traversal.**

**Memory Usage: 34 MB, less than 40.79% of C++ online submissions for N-ary Tree Level Order Traversal.**
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
    //DFS方法
    vector<vector<int> > ans;
    vector<vector<int>> levelOrder(Node* root) {
        if(root==NULL) return {};
        dfs(root,0);
        return ans;
    }
    void dfs(Node* root,int n)
    {
        if(n>=ans.size())
        {
            ans.push_back({});
        }
        ans[n].push_back(root->val);
        for(int i=0;i<root->children.size();i++)
        {
            dfs(root->children[i],n+1);
        }
    }
    
};
```
 
