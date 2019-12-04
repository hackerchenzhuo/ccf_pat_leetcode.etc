# 原创：leetcode 78. 子集【无序子集，使用不带标记的回溯】

 

**执行用时 : 8 ms, 在Subsets的C++提交中击败了97.63% 的用户**

**内存消耗 : 9.3 MB, 在Subsets的C++提交中击败了32.82% 的用户**

依然是那个思想：

# **回溯**

和以前的全排列不同，这次不需要记录是否访问过。也就是不需要额外的数组记录位置：

 

因为：

### 这里的子集内部没有顺序。对于没有顺序的题，按顺序来就ok

重点依然在这一句：

> 
<p>            tt.push_back(nums[i]);<br/>
            find(nums,i+1,tt);<br/>
            tt.pop_back();</p>

```c++
class Solution {
public:
    vector<vector<int> > ans; 
    vector<vector<int>> subsets(vector<int>& nums) {
        if(nums.size()<=0) return ans;
        vector<int> tt;
        find(nums,0,tt);
        return ans;
    }
    void find(vector<int>& nums,int begin,vector<int> &tt)
    {
        ans.push_back(tt);
        for(int i=begin;i<nums.size();i++)
        {
            {
            tt.push_back(nums[i]);
            find(nums,i+1,tt);
            tt.pop_back();
            }
        }
    }
};
```
 
