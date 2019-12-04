# 原创：leetcode 62. 不同路径【动态规划代表题】

对于这种有重复使用的题，肯定是要用动态规划的：

**执行用时 : 4 ms, 在Unique Paths的C++提交中击败了94.94% 的用户**

**内存消耗 : 9.1 MB, 在Unique Paths的C++提交中击败了5.14% 的用户**
```c++
class Solution {
public:
    int a,b;
    
    long long uniquePaths(int m, int n) {
        //先思考
        //递归？回溯？动态规划？自底向上，自顶向下？
        //重复走路，动态规划！！！
        if(m==0||n==0) return 0;
        a=m;b=n;
        vector<vector<long long> > ans(m+5,vector<long long>(n+5,0));
        long long res=go(1,1,ans);
        return res;
        
    }
    long long go(int x,int y,vector<vector<long long> >& t)
    {
        if(t[x][y]>0)
            return t[x][y];
        if(x==a&&y==b)
        {
            return 1;
        }
        long long ans=0;
        if(x<a)
            ans+=go(x+1,y,t);
        if(y<b)
            ans+=go(x,y+1,t);
        t[x][y]=ans;
        return ans;
    }
};
```

我可以保证这个测试数据绝对没超过20（题目给的是不超过100）

不信你看：
![](https://img-blog.csdnimg.cn/20190606174814560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

用英文版的leetcode测试：

我呵呵
![](https://img-blog.csdnimg.cn/2019060617513784.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

连标准程序都无法通过。。。20*20

 

官网给的标准答案：

也是动态规划，不过是反过来的，自顶向下：【自认为我的答案比标准答案好。**我是先判断再进入。官网是先进入再判断**】
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        int *dp[n];
        for(int i = 0; i < n; i++){
            dp[i] = (int*)malloc(m*sizeof(int));
            memset(dp[i], 0, m*sizeof(int));
        }
        return dpMethod(n-1, m-1, dp);
    }
private:
    int dpMethod(int n, int m, int **dp){
        if(n < 0 || m < 0) return 0;
        if(n == 0 || m == 0) return 1;
        if(dp[n][m] > 0) return dp[n][m];
        dp[n][m] = dpMethod(n-1, m, dp) + dpMethod(n, m-1, dp);
        return dp[n][m];
    }
};
```
> 
然后看leetcode国服：
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 1));
        for(int i = 1; i < m; i++) {
            for(int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```

# 好吧我还是太菜了。
