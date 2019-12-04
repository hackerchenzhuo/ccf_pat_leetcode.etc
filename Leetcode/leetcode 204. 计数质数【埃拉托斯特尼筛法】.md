# 原创：leetcode 204. 计数质数【埃拉托斯特尼筛法】

想法一：

是素数则吧倍数都置为非素数。

否则置1（非素数），遍历n次。

第19个案例超了。
```c++
class Solution {
public:
    int countPrimes(int n) {
        //0:质数 1：非质数
        int ans[n+1]={0};
        if(n<=2) return 0;
        //核心剪枝：每次把所以倍数都置1！！！
        //次级剪枝：根号即可
        for(int i=3;i<n;i++)
        {
            if(ans[i]) continue;//一定不是质数
            int flag=0;
            for(int j=2;j<=sqrt(i);j++)//找质因子即可
            {
                if(!ans[j]&&(i%j)==0)//j必须是质数,且i整除了j
                {
                    ans[i]=1;//不是质数
                    flag=1;//不是质数
                    break;
                }
            }
            if(!flag)
            {
                //是质数
                    int t=i*2;//倍数相加
                    for(int m=3;t<n;m++)
                    {
                        ans[t]=1;
                        t=m*i;
                    }
            }
        }
        
        int res=0;
        for(int i=2;i<n;i++)
        {
            if(!ans[i])res++;
        }
        return res;
    }
};
```

想法二：

**执行用时 : 44 ms, 在Count Primes的C++提交中击败了90.95% 的用户**

**内存消耗 : 14.8 MB, 在Count Primes的C++提交中击败了22.99% 的用户**

不要想复杂了。不要多余的步骤。

就在sqrt（n）内，求倍数。素数的反义词是倍数。把倍数都填满了，素数就浮现出来了。

从相反的角度思考问题，往往有更好的解法。

【**埃拉托斯特尼筛法**】
```c++
class Solution {
public:
    int countPrimes(int n) {
        //0:质数 1：非质数
        int ans[n+1]={0};
        if(n<=2) return 0;
        //核心剪枝：每次把所以倍数都置1！！！
        for(int i=2;i<=sqrt(n);i++)
        {
            if(ans[i]) continue;
           int t=i+i;
           while(t<n)
           {
               ans[t]=1;
               t+=i;
           }
        }
        
        int res=0;
        for(int i=2;i<n;i++)
        {
            if(!ans[i])res++;
        }
        return res;
    }
};
```

 
