# 原创：leetcode 51. N皇后【模板题】

**执行用时 : 8 ms, 在N-Queens的C++提交中击败了98.14% 的用户**

**内存消耗 : 10.8 MB, 在N-Queens的C++提交中击败了40.80% 的用户**

 

> 
<h3>N皇后经典问题【实在想不通为啥属于困难难度】</h3>
关键思想：爆搜剪枝——因为事先知道不可能在同一行/列，所以也就没必要一个格子一个格子地搜索，可以直接**以行或者列为单位**进行搜索。


> 
 判定语句：
if(ans[j]==i || abs(ans[j]-i)==abs(j-n))//在一对角上或者在一行上


 

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


 
