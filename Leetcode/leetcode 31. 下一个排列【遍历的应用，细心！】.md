# 原创：leetcode 31. 下一个排列【遍历的应用，细心！】

**执行用时 : 8 ms, 在Next Permutation的C++提交中击败了99.64% 的用户**

**内存消耗 : 8.7 MB, 在Next Permutation的C++提交中击败了80.36% 的用户**

**逻辑一定要理清楚。**

### 具体可以参考leetcode的官方教程：（我加了注解）
![](https://img-blog.csdnimg.cn/20190601164742757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 结合动图：（注意最后有一次排序（逆序），别忘了）

#### [图没了]=_=

> 
<ol>

- 设i是倒数第二个结点，j是倒数第一个。i--，j--，直到：
  
- 从右往左找到第一个拐点——**nums[i]第一次小于nums[j]的地方。**
- 然后固定i不动，j往右边寻路，找从右边数第一个刚好nums[j]**大于**nums[i]的 地方（易错点！！！！！nums[j]不能等于num[i]，不然交换没有意义，而且整个逻辑就崩了）。
- 然后交换完后，i的右边应该保持最小字典序，这样才能是刚好在上一个自动序之后。**不需要sort，reverse就行**。因为右边本来就是有序的。
</ol>

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        //15.22
        //找最后一个，numsj比numsi大的对。交换。
        int sz=nums.size();
        if(sz<=1) return;
        int i=sz-2,j=sz-1;
        while(i>=0)
        {
            if(nums[i]<nums[j])//找到了一个(此时i后面全是降序，可以说这里是拐点)
            {
                //反向寻路
                
                while(j<sz)
                {                    
                    if(nums[j]<=nums[i])//
                    {
                       //找到了右边数起第一个大于的
                       break;
                    }
                    j++;
                }
                //t是右边第一个不小于nums[i]的数
                 int t=j-1;//找到了
                //右边始终不小于
               swap(nums[i],nums[t]);
                //因为右边现在是降序，是最大的。我们需要最小的排列，所以需要反转。
               reverse(nums.begin()+i+1,nums.end());
               //开始反转
               return;         
            }
            i--;j--;
        }
        //此时还没找到，说明是降序的。
        sort(nums.begin(),nums.end());
        
    }
};
``` 

 
