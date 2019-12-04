# 原创：leetcode 326. 3的幂【如何不用循环？】

# **无脑方法：**

**循环**

执行用时 : 24 ms, 在Power of Three的C++提交中击败了93.99% 的用户

内存消耗 : 8.2 MB, 在Power of Three的C++提交中击败了13.87% 的用户
```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        //3的幂次方必然有3的幂次方作为因子；
        long long i=1;
        while(i<n)
        {
            i=3*i;
        }
        if(i!=n) return false;
        return true;
    }
};
```
# 有脑方法

 取对数。。。

执行用时 : 20 ms, 在Power of Three的C++提交中击败了96.36% 的用户

内存消耗 : 8.5 MB, 在Power of Three的C++提交中击败了5.11% 的用户
```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n==0) return false;
        //3的幂次方必然有3的幂次方作为因子；
        double i=log10(n)/log10(3);
        if(i==int(i)) return true;
        return false;
    }
};
```
 
