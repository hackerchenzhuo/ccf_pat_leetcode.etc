# 原创：leetcode 461. 汉明距离【二进制计算】

执行用时 : 0 ms, 在Hamming Distance的C++提交中击败了100.00% 的用户

内存消耗 : 8.3 MB, 在Hamming Distance的C++提交中击败了73.26% 的用户

```c++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int t=x^y;
        return gethan(t);
    }
    int gethan(int x)
    {
        int k=0;
        while(x>0)
        {
            if((x&1)==1)
            {
                k++;
            }
            x=x>>1;
        }
        return k;
    }
};
``` 
