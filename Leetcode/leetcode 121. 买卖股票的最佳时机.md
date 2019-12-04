# 原创：leetcode 121. 买卖股票的最佳时机

暴力法，时间O(n^2):

执行用时：**1220 ms**

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int sz=prices.size();
        int max=0;int t;
        for(int i=0;i<sz;i++)
        {
            for(int j=i+1;j<sz;j++)
            {
                if(prices[j]>prices[i]+max) 
                {
                    max=prices[j]-prices[i];
                }
            }
        }
        return max;
    }
};
```

一次遍历法：

执行用时 : 8 ms, 在Best Time to Buy and Sell Stock的C++提交中击败了98.77% 的用户

内存消耗 : 9.5 MB, 在Best Time to Buy and Sell Stock的C++提交中击败了37.14% 的用户

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int sz=prices.size();
        if(sz==0) return 0;
        int max=0;
        int minv=prices[0];
        for(int i=0;i<sz;i++)
        {
            if(prices[i]<minv) minv=prices[i];
                if(prices[i]>minv+max) 
                {
                    max=prices[i]-minv;
                }
        }
        return max;
    }
};
```

再优化一点点：

纪念一下第一次超过100%的。。。
![](https://img-blog.csdnimg.cn/20190514134125402.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size()==0) return 0;
        int max=0;
        int minv=prices[0];
        for(int i=0;i<prices.size();i++)
        {
            if(prices[i]<minv) minv=prices[i];
            else if(prices[i]>minv+max) 
                {
                    max=prices[i]-minv;
                }
        }
        return max;
    }
};
```
