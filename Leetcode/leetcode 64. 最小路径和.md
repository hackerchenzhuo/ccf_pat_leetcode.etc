# 原创：leetcode 64. 最小路径和

方法 1： 暴力

暴力就是利用递归，对于每个元素我们考虑两条路径，**向右走和向下走**，在这两条路径中挑选路径权值和较小的一个。

> 
有重复吗？
肯定有重复。


时间复杂度：

2^(m+n) 每次有两种选择，下或者右：右是n，下是m，所以是m+n；

 空间复杂度根据递归深度确定。

 

### 所以需要动态规划：

二维动态规划：根据每次只有两个移动方向的特点：从后往前依次判断，最后到达起点（当然从前往后也可以，但是自顶向下好一些）。<br/>**时间复杂度：**

只需要遍历一次：O（mn） 

**空间复杂度：**

O（mn）需要额外的矩阵

改进1：

使用一维数组存：【原理：每一行的数据只会被使用一次（被下一行使用）。所以覆盖是ok的】

改进2：

直接在原数组存。

**执行用时 : 8 ms, 在Minimum Path Sum的C++提交中击败了99.05% 的用户**

**内存消耗 : 10.7 MB, 在Minimum Path Sum的C++提交中击败了85.29% 的用户**
```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        //只有两条路
        if(grid.size()==0) return 0;
        for(int i=grid.size()-1;i>=0;i--)
            for(int j=grid[0].size()-1;j>=0;j--)
            {
                grid[i][j]=dp(grid,i,j);
            }
        return grid[0][0];
    }
    
    int dp(vector<vector<int>>& g,int &x,int &y)
    {
        int d=0,r=0;
        if(x+1<g.size()&&y+1==g[0].size()) return g[x][y]+g[x+1][y];
        if(y+1<g[0].size()&&x+1==g.size()) return g[x][y]+g[x][y+1];
        if(y+1<g[0].size()&&x+1<g.size()) return g[x][y]+min(g[x+1][y],g[x][y+1]);
        return g[x][y];
    }
};
```
 
