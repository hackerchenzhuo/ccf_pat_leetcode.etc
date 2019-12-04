# 原创：leetcode 88. 合并两个有序数组

 时间复杂度O（2n）。

分别是比较：n，一一赋值：n
```c++
class Solution {
    //19.51-
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        vector<int>tmp(m+n);
        int i=0,m1=0,n1=0;
        while(m1<m&&n1<n){
            if(nums1[m1]<nums2[n1]){
                tmp[i++]=nums1[m1++];
            }
            else{
                tmp[i++]=nums2[n1++];
            }
        }
        if(m1<m){
            while(m1<m){
                tmp[i++]=nums1[m1++];
            }}
            else{
                while(n1<n){
                tmp[i++]=nums2[n1++];
            }
            }
        nums1=tmp;
    }
};
```
 

 更好的办法：时间复杂度O（n），空间复杂度O（n）妙啊
```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int k = m+n-1;
        m--;
        n--;
        
        while(m >= 0 && n >= 0)
        {
            if(nums1[m] > nums2[n]) 
                nums1[k--] = nums1[m--];
            else
                nums1[k--] = nums2[n--];
        }
        
        while(n >= 0)
            nums1[k--] = nums2[n--];
    }
};
```
 
