# 原创：leetcode 22.括号生成【回溯】

对待这种问题，千万别暴力搜索，那样太笨了。

方法一：

**执行用时 : 20 ms, 在Generate Parentheses的C++提交中击败了67.40% 的用户**

**内存消耗 : 18.9 MB, 在Generate Parentheses的C++提交中击败了14.83%的用户**

第一个想到的是回溯法。每一次判别就ok。挺简单的。但是时间消耗比较久。可能是没有剪枝导致的。

但是这个方法是最容易理解的
```c++
class Solution {
public:
    vector<string> ans;
    vector<string> generateParenthesis(int n) {
        //回溯法 (后面的括号) 不可以大于 (前面的括号) 数量
        //即前面剩余的括号 i 不能多于后面剩余的括号 j 。
        dfs(n,n,"");
        return ans;
    }
    void dfs(int i,int j,string s)
    {
        if(!(i||j))//i和j都等于0了
        {
            ans.push_back(s);
            return;
        }  
        if(i>j||i<0||j<0) return;
        dfs(i-1,j,s+"(");
        dfs(i,j-1,s+")");
    }
    
};
```

 

 
