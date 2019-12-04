# 原创：leetcode 279. 完全平方数【动态规划 or 图论 】

给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

> 
<p>输入: n = 12<br/>
输出: 3 <br/>
解释: 12 = 4 + 4 + 4.</p>


> 
<p>输入: n = 13<br/>
输出: 2<br/>
解释: 13 = 4 + 9.</p>


 

方法1：

DP动态规划：

**执行用时 :160 ms, 在所有C++提交中击败了51.75%的用户**

**内存消耗 :11.4 MB, 在所有C++提交中击败了34.17%的用户**

（1）DP-1
```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, INT_MAX);
        dp[0] = 0;
        for(int i = 0; i <= n; i++) {
            for(int j = 1; i + j * j <= n; j++) {
                dp[i + j * j] = min(dp[i + j * j], dp[i] + 1);
            }
        }
        return dp[n];
    }
};
```
 

（2）DP-2
```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, 4);
        for(int i = 1; i * i <= n; i++)
            dp[i * i] = 1;
        for(int i = 1; i <= n; i++)
            for(int j = 1; j * j < i; j++)
            {
                dp[i] = min(dp[i], dp[i - j * j] + 1);
            }
        return dp[n];
    }
};
```

方法二：

前提：

**四平方和定理**。

> 
**Lagrange 四平方定理： 任何一个正整数都可以表示成不超过四个整数的平方之和。**


 
