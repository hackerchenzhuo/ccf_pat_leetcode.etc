# 原创：leetcode 55. 跳跃游戏【超级重要啊！！！！！！！！】

# 想法一：

递归：【第三次碰到了，。。。】

结果万万没想到啊！！！！超时了
![](https://img-blog.csdnimg.cn/20190605233230234.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
```c++
class Solution {
public:
    int ok=0;
    bool canJump(vector<int>& nums,int now=0) {
        //第三遍了啊！！！
        //加油 23:13
        if(ok) return true;
        if(now>=nums.size()-1) 
        {
            ok=1;
            return true;
        }
        if(nums[now]==0) return false;
        int flag=0;
        for(int i=1;i<=nums[now];i++)
        {
            flag=flag||canJump(nums,now+i);
            if(flag) 
            {
                ok=1;
                return true;
            }
        }
        return flag;
    }
};
```
 

怎么优化呢。。。剪枝？

我觉得这题要动态规划，不能无脑 

但是用了动态规划：**若判断不通就置0，防止重复搜索。**

**还是不行鸭！！！！**
```c++
class Solution {
public:
    int ok=0;
    
    bool canJump(vector<int>& nums)
    {
        vector<int> judge(nums.size(),1);
        return Jump(nums,0,judge);
    }
    bool Jump(vector<int>& nums,int now,vector<int>&judge ) {
        //第三遍了啊！！！
        //加油 23:13
        //剪枝+动态规划：记录当前位置后来能否走通
        if(ok) return true;
        if(now>=nums.size()-1) 
        {
            ok=1;
            return true;
        }
        if(!nums[now]||!judge[now]) return false;//当前是0或者已经判别过行不通了
        int flag=0;
        for(int i=1;i<=nums[now];i++)
        {
            flag=flag|Jump(nums,now+i,judge);
            if(flag) 
            {
                ok=1;
                return true;
            }
        }
        if(!flag) judge[now]=0;
        return flag;
    }
};
```

引用leetcode 官方的原话：

> 
这是一个动态规划问题，通常解决并理解一个动态规划问题需要以下 4 个步骤：
<ol>- **利用递归回溯解决问题**
- **利用记忆表优化（自顶向下的动态规划）**
- **移除递归的部分（自底向上的动态规划）**
- **使用技巧减少时间和空间复杂度**
</ol>

下面的所有解法都是正确的，但在时间和空间复杂度上有区别。

 

**优化一：每次先最大再最小。先迈步子大一点。 **

 

**可以从右到左的检查 nextposition ，理论上最坏的时间复杂度复杂度是一样的。但实际情况下，对于一些简单场景，这个代码可能跑得更快一些。直觉上，就是我们每次选择最大的步数去跳跃，这样就可以更快的到达终点。**

 

 万万没想到，就优化了这一步，居然通过了。
![](https://img-blog.csdnimg.cn/20190605235405185.png)

**提示：自顶向下以消除回溯！！！！！！！**

**从右至左计算。，就不需要再一层层回溯了。**

 

从右向左，一遍遍历。贪心的思想！！！！！依次查询，用一个变量记录目前最左端的good值。

**执行用时 : 12 ms, 在Jump Game的C++提交中击败了97.16% 的用户**

**内存消耗 : 9.8 MB, 在Jump Game的C++提交中击败了80.66% 的用户**

**简直了。不要太简单。**

```c++
class Solution {
public:
    bool canJump(vector<int>& nums)
    {
        //贪心的思想
        int tmp=nums.size()-1;
        for(int i=tmp;i>=0;i--)
        {
            if(i+nums[i]>=tmp) tmp=i;
        }
        if(tmp==0) return true;
        return false;
    }
};
``` 

自顶向下的好处是可以重复利用许多东西。 
