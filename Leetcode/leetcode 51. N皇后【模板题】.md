# 原创：leetcode 51. N皇后【模板题】

**执行用时 : 8 ms, 在N-Queens的C++提交中击败了98.14% 的用户**

**内存消耗 : 10.8 MB, 在N-Queens的C++提交中击败了40.80% 的用户**

 

> 
<h3>N皇后经典问题【实在想不通为啥属于困难难度】</h3>
关键思想：爆搜剪枝——因为事先知道不可能在同一行/列，所以也就没必要一个格子一个格子地搜索，可以直接**以行或者列为单位**进行搜索。


> 
 判定语句：
if(ans[j]==i || abs(ans[j]-i)==abs(j-n))//在一对角上或者在一行上

![](https://img-blog.csdnimg.cn/20190607211510848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 

> 
 图形化输出语句：
<p>vector&lt;vector&lt;string&gt;&gt; sss;<br/>
        for(int i=0;i&lt;res.size();i++)<br/>
        {<br/>
            vector&lt;string&gt; ss;<br/>
            for(int j=0;j&lt;N;j++)<br/>
            {<br/>
                string s="";<br/>
                for(int k=0;k&lt;N;k++)<br/>
                {<br/>
                    s+= k==res[i][j]? 'Q':'.';<br/>
                }<br/>
                ss.push_back(s);<br/>
            }<br/>
            sss.push_back(ss);<br/>
            <br/>
        }<br/>
        return sss;</p>


```c++
class Solution {
public:
    int N;
 
    vector<vector<int> >res;
    vector<vector<string>> solveNQueens(int n) {
        //N皇后问题。固定行
        //回溯
        N=n;
        vector<int> ans(N);
        find(0,ans);
        vector<vector<string>> sss;
        for(int i=0;i<res.size();i++)
        {
            vector<string> ss;
            for(int j=0;j<N;j++)
            {
                string s="";
                for(int k=0;k<N;k++)
                {
                    s+= k==res[i][j]? 'Q':'.';
                }
                ss.push_back(s);
            }
            sss.push_back(ss);
            
        }
        return sss;
    }
    void find(int n,vector<int> &ans)
    {
        if(n==N) 
        {
            //cout<<"1"<<endl;
            res.push_back(ans);
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
