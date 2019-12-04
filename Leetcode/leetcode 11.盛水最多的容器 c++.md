# 原创：leetcode 11.盛水最多的容器 c++

方法1：

暴力法。从前往后，每次检索 最长的区域*二者间最矮的高度。

时间复杂度O（n^2）

 ```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        if(height.size()<=1) return 0;
        else{
            int size=height.size();
            int l,r,max=0;
            for(l=0;l<size;l++){
                int hmax=0;
                for(r=size-l-1;r>0;r--){
                    if(height[l+r]<hmax) continue;
                    else hmax=height[l+r];
                    int key=min(height[l+r],height[l])*(r);
                    if(key>max)
                        max=key;
                }
            }
            return max;
        }
        
    }
};
```


 法二：

双指针法。每次取最优。

法一中有重复步骤。用法二可以避免重复。

**原理：两线段之间形成的区域总是会受到其中较短那条长度的限制。此外，两线段距离越远，得到的面积就越大。**

时间复杂度：O（n）

 ```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        if(height.size()<=1) return 0;
        else{
            int size=height.size();
            int l=0,r=size-1,max=0;
            while(l<r){
                int key=min(height[l],height[r])*(r-l);
                max=key>max?key:max;
                height[l]>height[r]?r--:l++;
            }
            return max;
            }
            
        }
        
    };
```