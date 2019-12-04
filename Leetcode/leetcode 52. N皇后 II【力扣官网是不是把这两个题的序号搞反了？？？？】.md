# 原创：leetcode 52. N皇后 II【力扣官网是不是把这两个题的序号搞反了？？？？】

**执行用时 : 4 ms, 在N-Queens II的C++提交中击败了98.21% 的用户**

**内存消耗 : 8.3 MB, 在N-Queens II的C++提交中击败了57.10% 的用户**

 

首先这个题目的难度根本不算困难好不好。。。

其次。。

为什么N皇后 II比N皇后 I还简单。。。。N皇后 I完全包括了N皇后 II好不好...

**加一个total计数就ok了。简单。依然是回溯的方法**

```c++
class Solution {
public:
    int N;
    int total=0;
    int totalNQueens(int n) {
        N=n;
        vector<int> ans(n);
        find(0,ans);
        return total;
    }
    void find(int n,vector<int> &ans)
    {
        if(n==N) 
        {
            //cout<<"1"<<endl;
            total++;
            return;
        }
        
        for(int i=0;i<N;i++)//只考虑行,对于这N列来说
        {
            int ok=1;
            for(int j=0;j<n;j++)
            {
                if(ans[j]==i || abs(ans[j]-i)==abs(j-n))//在一对角上或者在一行上
                {
                    ok=0;
                    break;
                }
 
            }
            if(ok)//没有冲突
                {
                    ans[n]=i;
                    find(n+1,ans);
                }
        }
    }
};
 
 
``` 
