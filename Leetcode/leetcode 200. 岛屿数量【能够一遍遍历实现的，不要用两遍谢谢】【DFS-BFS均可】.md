# 原创：leetcode 200. 岛屿数量【能够一遍遍历实现的，不要用两遍谢谢】【DFS/BFS均可】

**执行用时 :12 ms, 在所有C++提交中击败了98.96%的用户**

**内存消耗 :10.9 MB, 在所有C++提交中击败了81.05%的用户**

遇到1就DFS，并且岛屿数量+1.

```c++
class Solution {
public:
    int flag=0;//从2开始选填充标志
    int numIslands(vector<vector<char>>& grid) {
        //经典问题
        //并查集？
        //应该是DFS
        if(grid.size()==0) return 0;
        for(int i=0;i<grid.size();i++)//竖
        {
            for(int j=0;j<grid[i].size();j++)//横
            {
                if(grid[i][j]=='1')
                {
                DFS(grid,i,j);
                flag++;
                }
            }
        }
        return flag;
    }
  
    void DFS(vector<vector<char>>& grid,int n,int m)
    {
        if(grid[n][m]=='1')//没走过的大陆
        {
 
            grid[n][m]='2';//ok
            //继续
            if(n<grid.size()-1)
                DFS(grid,n+1,m);
            if(m<grid[n].size()-1)
                DFS(grid,n,m+1); 
            if(n>0)
            {
                DFS(grid,n-1,m);
            }
            if(m>0)
            {
                DFS(grid,n,m-1);
            }
        }
        else return;
    }
};
``` 
