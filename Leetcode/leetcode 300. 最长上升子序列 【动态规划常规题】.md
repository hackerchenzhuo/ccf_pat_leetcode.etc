# 原创：leetcode 300. 最长上升子序列 【动态规划常规题】

# 方法一：

执行用时 :52 ms, 在所有 C++ 提交中击败了66.18%的用户

内存消耗 :8.7 MB, 在所有 C++ 提交中击败了16.75%的用户

DP肯定可以解决这种问题的。

每个DP[i]记录到目前为止最大的上升子串长度。每次与前面i-1的DP[i]对比，若其大于**等于**当前DP的值，则更新。

时间复杂度：O（n^2） 空间复杂度：O（n）；
```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int sz=nums.size();
        if(sz==0) return 0;
        vector<int> dp(sz,1);
        int ans=1;
        for(int i=0;i<sz;i++)
        {
            for(int j=i-1;j>=0;j--)
            {
                if(nums[i]>nums[j]&&dp[j]>=dp[i])
                {
                    dp[i]=dp[j]+1;
                }
            }
            ans=max(dp[i],ans);
        }
        return ans;
    }
};
```

### 方法二：贪心+动态规划：使得整个数组的元素尽可能小
