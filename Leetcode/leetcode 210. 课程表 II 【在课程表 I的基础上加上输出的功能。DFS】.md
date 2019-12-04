# 原创：leetcode 210. 课程表 II 【在课程表 I的基础上加上输出的功能。DFS】

**执行用时 : 28 ms, 在Course Schedule II的C++提交中击败了99.15% 的用户**

**内存消耗 : 14 MB, 在Course Schedule II的C++提交中击败了12.54% 的用户**

依然使用DFS进行环的判别

 

核心语句：

> 
<p>        for(int j=0;j&lt;tmp[i].size();j++)<br/>
        {<br/>
            if(dfs(tmp[i][j],flag,tmp))//找需要的课程<br/>
            {<br/>
                continue;//这个地方没有回路<br/>
            }<br/>
            return false;<br/>
        }<br/>**        res.push_back(i);//这个课程push_back（即，在该课程的先修课都入队后，该课程已经可以入队）**</p>


 
