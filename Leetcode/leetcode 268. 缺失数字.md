# 原创：leetcode 268. 缺失数字

# 缺失数字

给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

示例 1:  
输入: [3,0,1]  
输出: 2  

示例 2:  
输入: [9,6,4,2,3,5,7,0,1]  
输出: 8  

说明: 你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?

## 解法1：

排序后比对值和下标是否对应
```c++
class Solution {
public:
    static bool cmp(const int&a,const int&b)
    {
        return a<b;
    }
    int missingNumber(vector<int>& nums) {
        sort(nums.begin(),nums.end(),cmp);
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]!=i)
                return i;
        }
        return nums.size();
    }
};
```

## 解法2：异或
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int res=nums.size();
        for(int i=0;i<nums.size();i++)
        {
            res^=nums[i];
            res^=i;
        }
        return res;
    }
};
```

## 解法3：等差数列求和

用数列和sum减去num中的数据，剩下的数据就是缺失的数据
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int sum=(nums.size()*(nums.size()+1))/2;
        for(int i=0;i<nums.size();i++)
        {
            sum-=nums[i];
        }
        return sum;
    }
};
```

## 解法4：
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int sum=0;
        for(int i=0;i<nums.size();i++)
        {
            sum=sum-nums[i]+i;
        }
        return sum+nums.size();
    }
};
```
