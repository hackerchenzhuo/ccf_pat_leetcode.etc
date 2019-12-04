# 原创：leetcode 79. 单词搜索【类似迷宫回溯】

 

**执行用时 : 24 ms, 在Word Search的C++提交中击败了99.00% 的用户**

**内存消耗 : 11 MB, 在Word Search的C++提交中击败了78.26% 的用户**

类似于迷宫回溯类问题。

### 上下左右依次寻路。并且使用vis数组作为访问标记。

使用引用加快速度。
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string &word) {
        //KMP算法的进化版吗。。
        //回溯算法，四方寻路。
        if(board.size()==0||word.size()==0) return false;
        vector<vector<int> > vis(board.size(),vector<int>(board[0].size(),0));//访问矩阵
        for(int i=0;i<board.size();i++)
        {
            for(int j=0;j<board[0].size();j++)
            {
                if(board[i][j]==word[0]) 
                    if(find(board,i,j,vis,1,word))
                        return true;
            }
        }
        return false;
    }
    bool find(vector<vector<char>>& board,int i,int j,vector<vector<int> > &vis,int len,string &word)
        //len：当前以及找到多长的了
    {
        if(len>=word.size())
        {
            return true;
        }
        else
        {
            vis[i][j]=1;
            if(i-1>=0&&!vis[i-1][j]&&board[i-1][j]==word[len]) 
            {
                if(find(board,i-1,j,vis,len+1,word)) return true;
            }
            if(i+1<board.size()&&!vis[i+1][j]&&board[i+1][j]==word[len]) 
            {
                if(find(board,i+1,j,vis,len+1,word)) return true;
            }
            if(j-1>=0&&!vis[i][j-1]&&board[i][j-1]==word[len]) 
            {
                if(find(board,i,j-1,vis,len+1,word)) return true;
            }
            if(j+1<board[0].size()&&!vis[i][j+1]&&board[i][j+1]==word[len]) 
            {
                if(find(board,i,j+1,vis,len+1,word)) return true;
            }
            vis[i][j]=0;
        }
        return false;
    }
};
```
 
