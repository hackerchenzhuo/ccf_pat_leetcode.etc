# 原创：leetcode 283. 移动零

 

Runtime: 12 ms, faster than 99.76% of C++ online submissions for Move Zeroes.

Memory Usage: 9.5 MB, less than 59.39% of C++ online submissions for Move Zeroes.

**相当于一次遍历，O（n）时间复杂度。没有用额外空间。**

> 
<p>     //双指针法补0<br/>
    //可以用双指针的情况：<br/>
    //同一个数组，不用额外的空间  </p>
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
    //双指针法补0
    //可以用双指针的情况：
    //同一个数组，不用额外的空间  
    int i=0,j=0;//i始终大于等于j
    for(;i<nums.size();i++)//i用来遍历
    {
        if(nums[i]!=0)//需要赋值给nums[j]
        {
            if(i!=j)
            {
                nums[j]=nums[i];
            }
            j++;
        }
        
    }
    while(j<nums.size())
    {
        nums[j++]=0;
    }
    }
};
```

 
