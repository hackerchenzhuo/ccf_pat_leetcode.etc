# 原创：leetcode 207. 课程表【拓扑排序找环】

**执行用时 : 20 ms, 在Course Schedule的C++提交中击败了99.80% 的用户**

**内存消耗 : 13.2 MB, 在Course Schedule的C++提交中击败了18.08% 的用户**

刚好看了刘汝佳老师的算法竞赛上面拓扑部分，想练练手。

这个算法的关键是flag访问数组中，使用了:-1/0/1三个标志

> 
<p><strong> //拓扑排序<br/>
//使用标志数组进行访问判别<br/>
//标志数组如果是1/0的，则会产生重复遍历的消耗<br/>
//如果是-1/0/1的，就可以避免重复计算。<br/>
 //1：从当前结点开始的拓扑是无环的<br/>
 //0：还未遍历过<br/>
//-1：正在遍历</strong></p>
 


 可以有效防止重复搜索。（flag为1说明从该结点出发已经计算过了）。
```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
          //拓扑排序
        //使用标志数组进行访问判别
        //标志数组如果是1/0的，则会产生重复遍历的消耗
        //如果是-1/0/1的，就可以避免重复计算。
        //1：从当前结点开始的拓扑是无环的
        //0：还未遍历过
        //-1：正在遍历
        vector<int> flag(numCourses,0);//标志
        vector<vector<int> > tmp(numCourses);
        if(prerequisites.empty()) return true; 
        for(int i=0;i<prerequisites.size();i++)
        {
            tmp[prerequisites[i][0]].push_back(prerequisites[i][1]);//对于该课程来说需要修的课
        }
        bool ans=true;;
        for(int i=0;i<numCourses;i++)
        {
            ans=ans&&dfs(i,flag,tmp);
        }
        return ans;
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
            if(dfs(tmp[i][j],flag,tmp))
            {
                continue;//这个地方没有回路
            }
            return false;
        }
        flag[i]=1;//该结点出去的每一个结点都访问完了，没有回路
        return true;
    }
};
```
拓展：[leetcode 210. 课程表 II 【在课程表 I的基础上加上输出的功能。DFS】](https://chenzhuo.blog.csdn.net/article/details/91128287)

 

### 方法二：根据入度判断

课程先后顺序可以理解为一个有向图，有解的条件是此图无环。因此我们可以依据其先后顺序构造有向图，并统计每门课程的入度（即其前一门课程的数量）。

然后将入度为0的所有课程压入栈中，然后将这些课程的下一门课程的入度减1，减完后入度为0则入栈。重复上述操作直到栈为空。** 如果最后存在入度不为为0的节点就说明有环，无解。**
```c++
class Solution {
public:
	vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
		vector<int>Indegree(numCourses);/* 统计各个节点的入度 */
		vector<vector<int>>graph(numCourses);/* 图的邻接矩阵 */
		queue<int>ZeroQ;/* 入度为0的节点的队列 */
		vector<int>ans,empty_ans;/* 结果数组 */
		int i, j, cnt = 0;
		int start, end;//start 依赖于 end, end 是 start 的先修课
		for (i = 0; i < prerequisites.size(); ++i) {
			start = prerequisites[i][0];
			end = prerequisites[i][1];
			graph[end].push_back(start);
			++Indegree[start];//入度加
		}
		/* 初始化队列 */
		for (i = 0; i < numCourses; ++i) {
			if (Indegree[i] == 0)
				ZeroQ.push(i);
		}
		while (!ZeroQ.empty()) {
			int v = ZeroQ.front();
			ans.push_back(v);
			ZeroQ.pop();
			++cnt;
			for (j = 0; j < graph[v].size(); ++j) {
				if (--Indegree[graph[v][j]] == 0)
                //v 是graph[v][j]这些课程的先修课。v移除代表在拓扑图中把这些先修课移除
					ZeroQ.push(graph[v][j]);
			}
		}
		if (cnt != numCourses)
			return empty_ans;
		return ans;
	}
};
```
 
