# 原创：leetcode 169. 求众数【四种方法】【摩尔投票法】

前三种方法：

> 
<p>//两次遍历，用map存：O（2n）<br/>
//先排序，再一次遍历O（nlgn + n）<br/>
//三次遍历，用空间换时间的数组存，O（3n） </p>


 

方法一：先排序

执行用时 : 40 ms, 在Majority Element的C++提交中击败了55.89% 的用户

内存消耗 : 11.1 MB, 在Majority Element的C++提交中击败了76.48% 的用户
```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int sz=nums.size();
        int sz2=sz/2;
        if(sz<=2) return nums[0];
        sort(nums.begin(),nums.end());
        int t=1;
        for(int i=1;i<sz;i++){
            if(nums[i]!=nums[i-1]){
                t=1;
            }
            else t++;
            if(t>sz2) return nums[i];
        }
        return 0;
    }
};
```
 

方法二：

用空间换时间的map存

执行用时 : 20 ms, 在Majority Element的C++提交中击败了99.15% 的用户

内存消耗 : 11.2 MB, 在Majority Element的C++提交中击败了45.97% 的用户
```c++
class Solution {
public://两次遍历，用map存：O（2n）
    //先排序，再一次遍历O（nlgn + n）
    //三次遍历，用空间换时间的数组存，O（3n）
    int majorityElement(vector<int>& nums) {
        int sz=nums.size();
        int sz2=sz/2;
        if(sz<=2) return nums[0];
        
        map<int,int> m;
        for(int i=0;i<sz;i++){
            m[nums[i]]++;
        }
        for(auto it=m.begin();it!=m.end();it++){
            if(it->second>sz2) return it->first;
        }
        return 0;
    }
};
```
 

 方法四：

leetcode上看见的：

摩尔投票法：**当一个数的重复次数超过数组长度的一半，每次将两个不相同的数删除，最终剩下的就是要找的数。**

 

**我个人的理解：一个数如果超过size/2，他必定会有连续出现的时候。**

执行用时 : 20 ms, 在Majority Element的C++提交中击败了99.15% 的用户

内存消耗 : 11.1 MB, 在Majority Element的C++提交中击败了67.11% 的用户

```c++
//Boyer-Moore Majority Vote algorithm.
// If we had some way of counting instances of the majority element as +1 and instances of any other element as -1, 
// summing them would make it obvious that the majority element is indeed the majority element.
class Solution {
public:
	int majorityElement(vector<int>& nums) { //本题最多的数字个数大于一半
        int ans=0;
        int count=0;
		for (int x : nums) {
            if(count == 0) ans=x;
            if(ans == x ) count++;
            else count--;
		}
		return ans;
	}
};
```
 
