# 原创：leetcode 350. 两个数组的交集 II【单重映射hash表】

 

**执行用时 : 20 ms, 在Intersection of Two Arrays II的C++提交中击败了50.66% 的用户**

**内存消耗 : 10.8 MB, 在Intersection of Two Arrays II的C++提交中击败了5.03% 的用户**

方法一：使用hash的map表映射。时间复杂度：O（n）。类似于三次遍历。

使用map&lt;int,vector&lt;int&gt;&gt; 的数据结构。有点麻烦

## **其实可以用单重hash 表-&gt;两次遍历**
```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        //hash映射交集。
        map<int,vector<int> > m;
        for(int i=0;i<nums1.size();i++)
        {
            if(m[nums1[i]].size()==0){
                m[nums1[i]].push_back(1);
                m[nums1[i]].push_back(0);
            }
            else m[nums1[i]][0]++;
        }
        for(int i=0;i<nums2.size();i++)
        {
            if(m[nums2[i]].size()==0) 
            {
                m[nums2[i]].push_back(0);
                m[nums2[i]].push_back(1);
                continue;
            }
            else m[nums2[i]][1]++;
        }
        vector<int> ans;
        int t=0;
        for(auto it=m.begin();it!=m.end();it++)
        {
            t=min(it->second[0],it->second[1]);
            while(t>0)
            {
                ans.push_back(it->first);
                t--;
            }
        }
        return ans;        
    }
};
```
 

 单重映射：

**执行用时 : 16 ms, 在Intersection of Two Arrays II的C++提交中击败了81.92% 的用户**

**内存消耗 : 9.9 MB, 在Intersection of Two Arrays II的C++提交中击败了5.03%的用户**

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        //hash映射交集。
        map<int,int> m;
        for(int i=0;i<nums1.size();i++)
        {
            m[nums1[i]]++;
        }
        vector<int> ans;
        for(int i=0;i<nums2.size();i++)
        {
            if(m[nums2[i]]==0) 
            {
                continue;
            }
            else {
                m[nums2[i]]--;
                ans.push_back(nums2[i]);
            }
        }
        return ans;        
    }
};
``` 
