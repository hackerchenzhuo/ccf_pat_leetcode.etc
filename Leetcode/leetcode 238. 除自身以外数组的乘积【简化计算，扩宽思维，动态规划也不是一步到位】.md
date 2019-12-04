# 原创：leetcode 238. 除自身以外数组的乘积【简化计算，扩宽思维，动态规划也不是一步到位】

# 方法一：使用除法

**执行用时 :56 ms, 在所有C++提交中击败了95.06%的用户**

**内存消耗 :12.4 MB, 在所有C++提交中击败了75.36%的用户**
```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> ans(nums.size());
        int t=1;
        int num_of_0=0;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]==0)
            {
                num_of_0++;
            }
            else
                t*=nums[i];
        }
        for(int i=0;i<nums.size();i++)
        {
            if(num_of_0>1||(num_of_0>0&&nums[i]!=0)) ans[i]=0;
            else if(nums[i]==0) ans[i]=t;
            else ans[i]=t/nums[i];
        }
        return ans;
    }
};
```

# 方法二：dfs 空间复杂度太高

> 
 DFS:    ans[i]=fron*last;//前面的*后面的


空间复杂度：O（n）

执行用时 :60 ms, 在所有C++提交中击败了88.68%的用户

内存消耗 :15.3 MB, 在所有C++提交中击败了5.01%的用户
```c++
class Solution {
public:
    vector<int> ans;
    vector<int> productExceptSelf(vector<int>& nums) {
        ans.resize(nums.size());
        dfs(1,0,nums);
        return ans;
    }
    int dfs(int fron,int i,vector<int>& nums)
    {
        if(i==ans.size()-1)
        {
            ans[i]=fron;
            return nums[i];//到底了，返回nums[i].
        }
        int tmp=fron*nums[i];
        int last=dfs(tmp,i+1,nums);
        ans[i]=fron*last;//前面的*后面的
        return nums[i]*last;//返回后面的
    }
};
```

方法三：两次遍历  空间复杂度O（1）

从左至右求每个元素除去该数之后左边元素的累乘

从右至左求每个元素除去该数之后右边元素的累乘

**执行用时 :68 ms, 在所有C++提交中击败了47.74%的用户**

**内存消耗 :12.5 MB, 在所有C++提交中击败了74.93%的用户**
```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> ans(nums.size());
        int k=1;
        for(int i=0;i<nums.size();i++)
        {
            ans[i]=k;
            k*=nums[i];
        }
        k=1;
        for(int i=nums.size()-1;i>=0;i--)
        {
            ans[i]*=k;
            k*=nums[i];
        }
        return ans;
    }
};
```

不太明白耗时为什么这么多。

用n代替nums.size()之后：【数组的size()每次都有**减法运算**，增加了耗时】

**执行用时 :56 ms, 在所有C++提交中击败了95.06%的用户**

**内存消耗 :12.6 MB, 在所有C++提交中击败了47.13%的用户**

 

附上国外某大佬代码：（把k省略了，妙啊）

**执行用时 :52 ms, 在所有C++提交中击败了98.08%的用户**

**内存消耗 :12.7 MB, 在所有C++提交中击败了42.84%的用户**
```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n=nums.size();
        vector<int> ans(n);
        ans[0]=1;
        for(int i=1;i<n;i++)
        ans[i]=nums[i-1]*ans[i-1];
        int r=1;
        for(int i=n-1;i>=0;i--)
        {
            ans[i]*=r;
            r*=nums[i];
        }
        return ans;
    }
};
```
 
