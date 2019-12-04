# 原创：240. 搜索二维矩阵 II【想清楚再写。查找问题，已经有序考虑二分！】

方法一：【我的方法】

以及好像看过类似的题，有印象。结果写了50分钟写出来个这么慢的。晕

> 
**执行用时 :1044 ms, 在所有C++提交中击败了7.05%的用户**
**内存消耗 :13.2 MB, 在所有C++提交中击败了5.06%的用户**
```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.size()==0||matrix[0].size()==0) return false;
        return search(matrix,target,0,matrix[0].size()-1);
    }
    //dfs搜索
    bool search(vector<vector<int>>& matrix, int &target,int x,int y)
    {
        if(matrix[x][0]>target) return false;
        int szy=matrix[0].size();
        int szx=matrix.size();
        int i=x,j=0;
        while(j<y)
        {
            if(j<y&&matrix[i][j+1]>target)
            {
                break;
            }
            j++;
        }
        while(i<szx)
        {
            if(matrix[i][j]==target)
            {
                return true;
            }
            if(i+1<szx&&matrix[i+1][j]>=target)
            {
                i++;
                break;
            }
            i++;//再加一次
        }
        if(i==szx)
        {
            
            return false;
            //右下角的元素一定是最大的。
            //但是最大的元素依然小于target
            //所以肯定无解了
        }
        else
        {
            cout<<i<<endl;
            return search(matrix,target,i,j);
        }
    }
};
```

思路：DFS方法

 ![](https://img-blog.csdnimg.cn/20190616200517822.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)  

方法二：

别人的方法：O（m+n）

**执行用时 :76 ms, 在所有C++提交中击败了96.54%的用户**

**内存消耗 :13 MB, 在所有C++提交中击败了5.06%的用户**

> 
<p>●从最右上角的元素开始找，如果这个元素比target大，则说明找更小的，往左走；如果这个元素比target小，则说明应该找更大的，往下走。<br/>
●画个图看代码就很容易理解，总之就是从右上角开始找，如果矩阵的元素小了就往下走，如果矩阵元素大了就往左走。如果某个时刻相等了，就说明找到了，如果一直走出矩阵边界了还没找到，则说明不存在。</p>


 ![](https://img-blog.csdnimg.cn/20190616200949160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

自己总是想的太复杂了。。应该想清楚再下笔。

方法三：在方法二的基础上进一步优化：二维数组的二分查找！
```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.size() == 0 || matrix[0].size() == 0) return false;
        const int M = matrix.size(), N = matrix[0].size();
        int i = M - 1, j = 0;
        while (i >= 0 && j < N) {
            if (matrix[i][j] == target) {
                return true;
            } else if (matrix[i][j] < target) {
                ++j;
            } else {
                --i;
            }
        }
        return false;
    }
};
```

时间复杂度降低到O(logm+logn).
