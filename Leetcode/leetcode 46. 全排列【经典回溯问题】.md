# 原创：leetcode 46. 全排列【经典回溯问题】

一次通过

执行用时 : 16 ms, 在Permutations的C++提交中击败了96.99% 的用户

内存消耗 : 9.6 MB, 在Permutations的C++提交中击败了37.50% 的用户

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> permute(vector<int>& nums) {
        //全排列问题，回溯ok
        const int sz=nums.size();
        vector<int> flag(sz,0);//访问标志
        vector<int> t;
        dfs(nums,0,sz,flag,t);
        return ans;
    }
    void dfs(vector<int>& nums,int i,const int &sz,vector<int> &flag,vector<int> &k)//i:当前位置，sz：最大的大小
    {
        if(i>=sz)
        {
            ans.push_back(k);
            return;
        }
        for(int j=0;j<sz;j++)
        {
            if(!flag[j])//未访问过
            {
                //标记为访问
                flag[j]=1;
                k.push_back(nums[j]);
                dfs(nums,i+1,sz,flag,k);
                k.pop_back();
                flag[j]=0;
            }
        }
    }
};
```

改进：【参考leetcode 英文版上最高效方法（比我少一个变量i，没有定义全局变量。其他差不多）】
```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        
        vector<vector<int>> lists;
        vector<int> item;
        vector<int> visited(nums.size(), 0);
        backtracking(nums, lists, item, visited);
        return lists;
        
    }
    
    void backtracking(vector<int>& nums, vector<vector<int>>& lists, vector<int>& item, vector<int>& visited){
        if(item.size() == nums.size())
        {
            lists.push_back(item);
        }
        else
        {
            for(int i = 0; i < nums.size(); i++)
            {
                if(visited[i] == 1) continue;
                visited[i] = 1;
                item.push_back(nums[i]);
                backtracking(nums, lists, item, visited);
                
                //回溯到上一步，去掉当前节点
                item.pop_back();
                visited[i] = 0;
            }
        }
    }
};
```
 
