# 原创：leetcode 171. Excel表列序号

执行用时 : 4 ms, 在Excel Sheet Column Number的C++提交中击败了99.20%的用户

内存消耗 : 8.3 MB, 在Excel Sheet Column Number的C++提交中击败了20.26% 的用户

 
```c++
class Solution {
public:
    int titleToNumber(string s) {
        int sz=s.size(),ans=0;
        for(int i=0;i<sz;i++)
        {
            ans+=(s[i]-'A'+1)*pow(26,sz-i-1);
        }
        return ans;
    }
};
```
 

 
