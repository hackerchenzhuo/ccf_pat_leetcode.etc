# 原创：leetcode 53. 最大子序和

不来花里胡哨的分治，做出来才是王道

解法一：（best）

 ```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum = nums[0];
        int maxSum = sum;
        for(int i=1; i<nums.size(); i++)
        {
            sum = (sum>0 ? sum : 0) + nums[i];
            maxSum = max(maxSum,sum);
        }
        return maxSum;
    }
};
```

解法二：

 ```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        vector<int>d(n,0);
        d[0]=nums[0];
        int max=d[0];
        for(int i=1;i<n;++i)
        {
            if(d[i-1]<0)
                d[i]=nums[i];
            else
                d[i]=d[i-1]+nums[i];
            if(d[i]>max)
             max=d[i];
            
        }
   return max;
        
    }
};
```


