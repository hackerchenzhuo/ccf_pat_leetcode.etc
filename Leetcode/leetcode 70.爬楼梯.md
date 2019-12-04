# 原创：leetcode 70.爬楼梯

不要写专门的递归函数，没必要。

我最开始的代码：

 ```c++
class Solution {
public:
    map<int,int> m;
    int climbStairs(int n) {
        return pa(n);
    }
    int pa(int x){
        if(x<0) return 0;
        else if(m[x]!=0) {
            return m[x];
        }
        else if(x==0) {
            return 1;
        }
        else {
            m[x]=pa(x-1)+pa(x-2);
            return m[x];
        }
        
    }
};
```

 参考代码：
```c++
class Solution {
public:
    int climbStairs(int n) {
        int dp[n + 3];
        dp[1] = 1;
        dp[2] = 2;
        
        for(int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
};
```
 
