# 原创：leetcode 221. 最大正方形【动态规划+避免多余计算】

**执行用时 :12 ms, 在所有C++提交中击败了100.00%的用户**

**内存消耗 :10.7 MB, 在所有C++提交中击败了92.82%的用户**

 

> 
<p><strong>        //动态规划问题<br/>
        //看了题解才想出来。<br/>
        //惭愧</strong></p>
**        //记录最大边长就行(避免多余的计算！！！！)**

![](https://img-blog.csdnimg.cn/20190615224815269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 

 

**设二维数组dp[m][n]，其中dp[i][j]表示以坐标(i,j)为右下角元素的最大正方形的边长。**

**通过观察我们可以看出当前位置的最大正方形边长为上，左，左上三个位置最大正方形边长的最小值+1。（必须这三个正方形同时满足&amp;&amp;该位置matrix[i][j]==1 的条件下，最大边长）**

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        if(matrix.size()==0) return 0;
        //动态规划问题
        //看了题解才想出来。
        //惭愧
        int dp[matrix.size()][matrix[0].size()];
        memset(dp,0,sizeof(dp));
        int ans=0;//最大值
        //防止重复判断
        for(int i=0;i<matrix.size();i++)
        {
            if(matrix[i][0]=='1') 
            {
                dp[i][0]=1;
                ans=1;
            }
        }
        for(int j=0;j<matrix[0].size();j++)
        {
            if(matrix[0][j]=='1') 
            {
                dp[0][j]=1;  
                ans=1;
            }
        }
        //开始
        //记录最大边长就行(避免多余的计算！！！！)
        for(int i=1;i<matrix.size();i++)
        {
            for(int j=1;j<matrix[0].size();j++)
            {
                if(matrix[i][j]=='1')
                {
                    dp[i][j]=min(dp[i-1][j-1],min(dp[i][j-1],dp[i-1][j]))+1; 
                    if(dp[i][j]>ans)
                    {
                        ans=dp[i][j];
                    }
                }
            }
        }
        return pow(ans,2);
    }
};
``` 
