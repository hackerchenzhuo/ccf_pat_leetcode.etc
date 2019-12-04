# 原创：leetcode 49. 字母异位词分组【标准化】

刚好今天看了算法竞赛里面的map标准化问题就碰到这题，运气也是挺好。

做起来很舒服呀

先排序，再比对。

**执行用时 : 84 ms, 在Group Anagrams的C++提交中击败了63.50% 的用户**

**内存消耗 : 20.1 MB, 在Group Anagrams的C++提交中击败了39.45% 的用户**

```c++
class Solution {
public:
    vector<vector<string> > groupAnagrams(vector<string>& strs) {
        //标准化的练手题 22:25
        
        map<string,vector<string> > m;
        
        vector<vector<string> > ans;
        if(strs.size()==0) return ans;
        for(auto it=strs.begin();it!=strs.end();it++)
        {
            m[deal(*it)].push_back(*it);
        }
        for(auto it=m.begin();it!=m.end();it++)
        {
            vector<string> tmp;
            for(auto t=(it)->second.begin();t!=(it)->second.end();t++)
            {
                tmp.push_back(*t);
            }
            ans.push_back(tmp);
        }
        return ans;
    }
    string deal(string &s)
    {
        string ans=s;
        sort(ans.begin(),ans.end());
        return ans;
    }
};
``` 
