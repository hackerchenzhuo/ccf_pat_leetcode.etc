# 原创：leetcode 191. 位1的个数

解法一：

bitset

执行用时 : 8 ms, 在Number of 1 Bits的C++提交中击败了93.71% 的用户

内存消耗 : 8.2 MB, 在Number of 1 Bits的C++提交中击败了14.97% 的用户
```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        bitset<32> a(n);
        int ans=0;
        for(int i=0;i<32;i++)
        {
            if(a[i]) ans++;
                
        }
        return ans;
    }
};
```
 

解法二：移位

执行用时 : 8 ms, 在Number of 1 Bits的C++提交中击败了93.71% 的用户

内存消耗 : 8.4 MB, 在Number of 1 Bits的C++提交中击败了5.21% 的用户
```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans=0;
        for(int i=0;i<32;i++)
        {
            ans+=(n>>i)&1;
                
        }
        return ans;
    }
};
```
 
