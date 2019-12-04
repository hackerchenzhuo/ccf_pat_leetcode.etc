# 原创：leetcode 189. 旋转数组【经典问题，两次逆序】

执行用时 : 24 ms, 在Rotate Array的C++提交中击败了97.74% 的用户

内存消耗 : 9.5 MB, 在Rotate Array的C++提交中击败了52.70% 的用户

经典问题

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        //如此经典的题!!!!
        //两次逆序！！！！！
        //一次全局，一次分叉
        k=k%nums.size();
        reverse(0,nums.size()-1,nums);
        reverse(0,k-1,nums);
        reverse(k,nums.size()-1,nums);
    }
    void reverse(int a,int b,vector<int>&nums)
    {
        int t;
        while(a<b)
        {
            t=nums[a];
            nums[a]=nums[b];
            nums[b]=t;
            a++;
            b--;
        }
    }
};
``` 
