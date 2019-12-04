执行用时 : 68 ms, 在Combination Sum的C++提交中击败了31.33% 的用户

内存消耗 : 17.7 MB, 在Combination Sum的C++提交中击败了28.48% 的用户

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        //又是dfs 回溯
        //已知都是正数
        dfs(candidates,target,{},0);
        return ans;
    }
    void dfs(vector<int>& c, int t, vector<int> k,int now)
    {
        if(t==0) 
        {
            ans.push_back(k);
            return;
        }
        if(t<0) return;
        for(int i=now;i<c.size();i++)//now的意义是避免重复使用
        {
            k.push_back(c[i]);
            dfs(c,t-c[i],k,i);
            k.pop_back();//回溯     
        }
    }
};
```

加上剪枝：【如果小于0就没必要继续了】

        for(int i=now;i<c.size();i++)//now的意义是避免重复使用
        {
            int kk=t-c[i];
            if(kk<0) continue;
            k.push_back(c[i]);
            dfs(c,kk,k,i);
            k.pop_back();//回溯     
        }
```
 结果还行：

执行用时 : 24 ms, 在Combination Sum的C++提交中击败了87.09% 的用户

内存消耗 : 11.3 MB, 在Combination Sum的C++提交中击败了56.49% 的用户

 

再改为引用调用
```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        //又是dfs 回溯
        //已知都是正数
        vector<int> a;
        dfs(candidates,target,a,0);
        return ans;
    }
    void dfs(vector<int>& c, int t, vector<int> &k,int now)
    {
        if(t==0) 
        {
            ans.push_back(k);
            return;
        }
        if(t<0) return;
        for(int i=now;i<c.size();i++)//now的意义是避免重复使用
        {
            int kk=t-c[i];
            if(kk<0) continue;
            k.push_back(c[i]);
            dfs(c,kk,k,i);
            k.pop_back();//回溯     
        }
    }
};
```
执行用时 : 20 ms, 在Combination Sum的C++提交中击败了95.67% 的用户

内存消耗 : 9.7 MB, 在Combination Sum的C++提交中击败了86.08% 的用户

 

还行、

