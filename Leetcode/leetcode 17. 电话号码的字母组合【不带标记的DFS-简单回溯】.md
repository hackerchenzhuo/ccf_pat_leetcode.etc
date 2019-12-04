# 原创：leetcode 17. 电话号码的字母组合【不带标记的DFS-简单回溯】

 

**执行用时 : 4 ms, 在Letter Combinations of a Phone Number的C++提交中击败了96.68% 的用户**

**内存消耗 : 8.8 MB, 在Letter Combinations of a Phone Number的C++提交中击败了28.24% 的用户**
```c++
class Solution {
public:
    vector<string> ans;
    vector<string> tmp;
    int sz;
    vector<string> letterCombinations(string digits) {
        tmp={"","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        sz=digits.size();
        if(sz==0) return ans;
        dfs(digits,0,"");
        return ans;
    }
    void dfs(string &digits,int i,string s)//i 到哪一层了  sz最大
    {
        if(i==sz)//到底了
        {
            ans.push_back(s);
            return;
        }
        for(int j=0;j<tmp[digits[i]-'1'].size();j++)
        {
            string ss=s;
            ss+=tmp[digits[i]-'1'][j];
            dfs(digits,i+1,ss);
        }
    }
    
};
```


优化：

中间**变量SS**是没必要的。如果担心改变了s的话，**可以在传参的时候累加**

执行用时 : 4 ms, 在Letter Combinations of a Phone Number的C++提交中击败了96.68% 的用户

内存消耗 : 8.5 MB, 在Letter Combinations of a Phone Number的C++提交中击败了75.40% 的用户  


```c++
        for(int j=0;j<tmp[digits[i]-'1'].size();j++)
        {
            dfs(digits,i+1,s+tmp[digits[i]-'1'][j]);
        }
```
