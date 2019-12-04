# 原创：leetcode 198. 打家劫舍

一开始肯定是想用递归做：**56 / 69** 个通过测试用例

超时不可避免。

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        
        int sz=nums.size();
        if(sz==0)return 0;
        return get(nums,sz-1);
    }
    
    int get(vector<int>& nums,int n)
    {
        if(n==1)
        {
            return max(nums[1],nums[0]);
        }
        if(n==0)
        {
            return nums[0];
        }
        
        return max(get(nums,n-1),get(nums,n-2)+nums[n]);
    }
};
```

改动态规划？重复利用：(爬楼梯升级版)

 注意：递归和动态规划区别：递归从后往前。动态规划从前往后：！！！！

**执行用时 : 4 ms, 在House Robber的C++提交中击败了97.83% 的用户**

**内存消耗 : 8.7 MB, 在House Robber的C++提交中击败了72.94% 的用户**

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        
        int sz=nums.size();
        if(sz==0)return 0;
        if(sz==1) return nums[0];
        if(sz==2)return max(nums[0],nums[1]);
        
        // return get(nums,sz-1);
        int ans[sz];
        ans[0]=nums[0];ans[1]=max(nums[0],nums[1]);
        for(int i=2;i<sz;i++)
        {
            ans[i]=max(ans[i-1],ans[i-2]+nums[i]);
        }
        return ans[sz-1];
    }
``` 
