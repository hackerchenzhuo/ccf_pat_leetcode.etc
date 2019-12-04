# 原创：leetcode 210. 课程表 II 【在课程表 I的基础上加上输出的功能。DFS】

**执行用时 : 28 ms, 在Course Schedule II的C++提交中击败了99.15% 的用户**

**内存消耗 : 14 MB, 在Course Schedule II的C++提交中击败了12.54% 的用户**

依然使用DFS进行环的判别

 

核心语句：

> 
<p>        for(int j=0;j&lt;tmp[i].size();j++)<br/>
        {<br/>
            if(dfs(tmp[i][j],flag,tmp))//找需要的课程<br/>
            {<br/>
                continue;//这个地方没有回路<br/>
            }<br/>
            return false;<br/>
        }<br/>**        res.push_back(i);//这个课程push_back（即，在该课程的先修课都入队后，该课程已经可以入队）**</p>

```c++
 
class Solution {
public:
    vector<int> res;
    vector<int>  findOrder(int numCourses, vector<vector<int>>& prerequisites) {
          //拓扑找环
        //使用标志数组进行访问判别
        //标志数组如果是1/0的，则会产生重复遍历的消耗
        //如果是-1/0/1的，就可以避免重复计算。
        //1：从当前结点开始的拓扑是无环的
        //0：还未遍历过
        //-1：正在遍历
        
        //拓扑排序
        //在找环的基础上输出
        vector<int> flag(numCourses,0);//标志
        vector<vector<int> > tmp(numCourses);
        if(numCourses==0) return {}; 
        for(int i=0;i<prerequisites.size();i++)
        {
            tmp[prerequisites[i][0]].push_back(prerequisites[i][1]);//把该课程的先修课压入
        }
        bool ans=true;;
        for(int i=0;i<numCourses;i++)
        {
            if(!flag[i])//还没有访问过
                ans=ans&&dfs(i,flag,tmp);
        }
        if(ans)
        {
            for(int i=0;i<flag.size();i++)
            {
                if(!flag[i])//没有访问过
                {
                    res.push_back(i);   
                }
            }
            return res;
        }
        return {};
    }
    
    bool dfs(int i,vector<int> &flag,vector<vector<int> > &tmp)
    {
        if(flag[i]==-1)//回路.有环
        {
            return false;
        }
        if(flag[i]==1)
        {
            return true;//可以确定从该结点出发没有回路   
        }
        //第一次访问
        flag[i]=-1;//正在访问
        
        for(int j=0;j<tmp[i].size();j++)
        {
            if(dfs(tmp[i][j],flag,tmp))//找需要的课程
            {
                continue;//这个地方没有回路
            }
            return false;
        }
        res.push_back(i);//这个课程入队
        flag[i]=1;//该结点出去的每一个结点都访问完了，没有回路
        return true;
    }
};
```
 
