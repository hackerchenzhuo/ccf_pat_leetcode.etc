# 原创：leetcode 56. 合并区间【不能在c++类中定义cmp】

方法一：O（nlogn）

sort 函数的功能很易于扩展，我们可以给它一个比较函数，让它按我们希望的方式工作。

> 
    如果想要自定义比较函数，就像这样：
    bool less_int(int a,int b){
        return b&lt;a;
    }


**执行用时 : 32 ms, 在Merge Intervals的C++提交中击败了62.40% 的用户**

**内存消耗 : 13.2 MB, 在Merge Intervals的C++提交中击败了5.08% 的用户**

 万万没想到啊，c++的类成员函数不能做sort的比较函数！！！！！

只能用lamba表达式了：

> 
** sort(tmp.begin(),tmp.end(),[](zb a,zb b){if(a.x==b.x)return a.left&lt;b.left;return a.x&lt;b.x;});**


主要意思就是用结构体储存区间的起始和结束位置，起始置为1，结束置为2，然后统一排序，根据起始和结束的数量是否匹配来判定重合。 
```c++
class Solution {
public:
    struct zb{
      int x;
      int left;//左边：1 右边：2
      zb(int a,int b)
      {
          x=a;left=b;
      }
    };
    vector<vector<int> > merge(vector<vector<int> >& intervals) {
        //坐标打表
 
        vector<zb> tmp;
        vector<vector<int> > ans;
        vector<int> res;
        for(int i=0;i<intervals.size();i++)
        {
            tmp.push_back({intervals[i][0],1});
            tmp.push_back({intervals[i][1],2});//右区间用2
        }
        sort(tmp.begin(),tmp.end(),[](zb a,zb b){if(a.x==b.x)return a.left<b.left;return a.x<b.x;});
        //cmp的目的是定义什么是小于
        int l=0;
 
        for(int i=0;i<tmp.size();i++)
        {
            if(tmp[i].left==1)
            {
                l++;
                if(l==1)
                {
                    res.push_back(tmp[i].x);
                }
            }
            else l--;
            if(l==0) 
            {
                res.push_back(tmp[i].x);
                ans.push_back(res);
                res.clear();
            }
        }
        return ans;
    }
};
```

 

方法二： 直接将原来的数组按左端排序，如果子元组的右端大于右边子元组的左端，那么合并，直到不满足的时候创建新的元组。

**但是不知道为什么这种方法很慢。**

执行用时 : 204 ms, 在Merge Intervals的C++提交中击败了10.32% 的用户

内存消耗 : 27.3 MB, 在Merge Intervals的C++提交中击败了5.08% 的用户

```c++
class Solution {
public:
 
    vector<vector<int> > merge(vector<vector<int> >& intervals) {
        vector<vector<int> >ans;
        if(intervals.size()==0) return ans;
        sort(intervals.begin(),intervals.end(),[](vector<int> a,vector<int> b){if(a[0]==b[0]) return a[1]>b[1];return a[0]<b[0];});//重定义小于
        
        int l=intervals[0][0];
        int r=intervals[0][1];
        for(int i=1;i<intervals.size();i++)
        {
            if(r>=intervals[i][0]) 
            {
                if(r<intervals[i][1]) r=intervals[i][1];
            }
            else
            {
                vector<int> tmp(2);
                //tmp.push_back(l);
                // tmp.push_back(r);
                tmp[0]=l;tmp[1]=r;
                ans.push_back(tmp);
                l=intervals[i][0];
                r=intervals[i][1];
            }
        }
                vector<int> tmp(2);
                //tmp.push_back(l);
                // tmp.push_back(r);
                tmp[0]=l;tmp[1]=r;
        ans.push_back(tmp);
        return ans;
        
    }
};
```

# 参考方法！；

这个方法不需要定义中间数组，直接在原数组上操作，方便和块了很多（无法运行，只是传授概念）

```c++
class Solution {
public:
    vector<Interval> merge(vector<Interval>& intervals) {
        if (intervals.empty()) return {};
        sort(intervals.begin(), intervals.end(), [](Interval &a, Interval &b) {return a.start < b.start;});
        vector<Interval> res{intervals[0]};
        for (int i = 1; i < intervals.size(); ++i) {
            if (res.back().end < intervals[i].start) {
                res.push_back(intervals[i]);
            } else {
                res.back().end = max(res.back().end, intervals[i].end);
            }
        }   
        return res;
    }
};
``` 
