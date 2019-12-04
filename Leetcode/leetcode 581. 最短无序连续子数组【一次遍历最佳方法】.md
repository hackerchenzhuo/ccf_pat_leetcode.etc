# 原创：leetcode 581. 最短无序连续子数组【一次遍历最佳方法】

方法一、先sort再比对。

执行用时 : 80 ms, 在Shortest Unsorted Continuous Subarray的C++提交中击败了34.15% 的用户

内存消耗 : 11.4 MB, 在Shortest Unsorted Continuous Subarray的C++提交中击败了69.79% 的用户

```c++
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        vector<int> tmp(nums);
        sort(tmp.begin(),tmp.end());
        int a=nums.size(),b=0;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]!=tmp[i]) {
                a=i;break;
            }
                
        }
        for(int j=nums.size()-1;j>=0;j--)
        {
            if(nums[j]!=tmp[j])
            {
                b=j;break;
            }
        }
        if(a>=b+1)
            return 0;
        return b-a+1;
    }
};
```

方法二、

一次遍历

【找到**从前往后**最后一个比前半部分**当前最大值**小的】

【找到**从后往前**最后一个比后半部分**当前最小值**大的】

执行用时 : 36 ms, 在Shortest Unsorted Continuous Subarray的C++提交中击败了97.79% 的用户

内存消耗 : 10.4 MB, 在Shortest Unsorted Continuous Subarray的C++提交中击败了91.37% 的用户
```c++
 
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n=nums.size(),a=nums[0],b=nums[n-1],l=-1,r=-2;
        for(int i=1;i<n;i++){
            a=max(a,nums[i]);
            b=min(b,nums[n-1-i]);
            if(a!=nums[i])r=i;
            if(b!=nums[n-1-i])l=n-1-i;
        }
        return r-l+1;
    }
};
```
 
