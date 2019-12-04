# 原创：leetcode 152. 乘积最大子序列【动态规划】

**执行用时 :4 ms, 在所有C++提交中击败了98.63%的用户**

**内存消耗 :9.3 MB, 在所有C++提交中击败了9.54%的用户**

和最大连续子串，上升子串不同，这个题需要定义两个dp数组。分别存到目前为止最小/最大的值。

这样的目的是：

对于负数的乘积，当然是越小越好（这样绝对值越大）。

对于正数的乘积，当然是越大越好。

**而每当遇到负数，则二者交换。**

**以实现以i位置结尾，**目前为止最小/最大的值。
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        //动态规划问题
        //双极值。min和max
        //遇到负数交换
        if(nums.size()==0) return 0;
        vector<int> max1(nums.size(),0);//以i结尾最大的串
        vector<int> min1(nums.size(),0);//以i结尾最小的串
        max1[0]=nums[0];min1[0]=nums[0];
        int ans=max1[0];
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]>=0)
            {
                max1[i]=max(nums[i],max1[i-1]*nums[i]);
                min1[i]=min(nums[i],min1[i-1]*nums[i]);
                if(ans<max1[i])
                    ans=max1[i];
            }
            else if(nums[i]<0)
            {
                max1[i]=max(nums[i],min1[i-1]*nums[i]);
                min1[i]=min(nums[i],max1[i-1]*nums[i]);
                if(ans<max1[i])
                    ans=max1[i];
            }
        }
        return ans;
    }
};
```
 
