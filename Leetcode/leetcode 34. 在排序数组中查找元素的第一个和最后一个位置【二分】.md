# 原创：leetcode 34. 在排序数组中查找元素的第一个和最后一个位置【二分】

二分法【我很疑惑这个题为什么是中等难度】

执行用时 : 12 ms, 在Find First and Last Position of Element in Sorted Array的C++提交中击败了94.74% 的用户

内存消耗 : 10.5 MB, 在Find First and Last Position of Element in Sorted Array的C++提交中击败了73.95% 的用户
```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        //easy
        if(nums.size()<=0) return {-1,-1};
        vector<int> ans=bs(nums,target,0,nums.size()-1);
        return ans;
    }
    vector<int> bs(vector<int>& nums,int &t,int i,int j)
    {
        
        if(i>j) return {-1,-1};
        int k=(i+j)/2;
        if(nums[k]==t)
        {
            int a=k,b=k;
            while(a-1>=0&&nums[a-1]==t)
            {
                a--;
            }
            while(b+1<nums.size()&&nums[b+1]==t)
            {
                b++;
            }
            return {a,b};
        }
        if(nums[k]>t) return bs(nums,t,i,k-1);
        else return bs(nums,t,k+1,j);
    }
    
};
```
 

 

听说正确的做法应该是多次二分。。。 
