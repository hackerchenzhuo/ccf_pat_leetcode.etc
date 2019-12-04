# 原创：leetcode 118. 杨辉三角【让每一次循环变得有意义】

执行用时 : 4 ms, 在Pascal's Triangle的C++提交中击败了98.60% 的用户

内存消耗 : 8.9 MB, 在Pascal's Triangle的C++提交中击败了8.35% 的用户

```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans;
        if(numRows==0) return ans;
        vector<int>t1;t1.push_back(1);ans.push_back(t1);
        for(int i=1;i<numRows;i++)
        {
            vector<int>t;t.push_back(1);
            for(int j=0;j<ans[i-1].size()-1;j++)
            {
                t.push_back(ans[i-1][j]+ans[i-1][j+1]);
            }
            t.push_back(1);
            ans.push_back(t);
            
        }
        return ans;
    }
};
``` 
