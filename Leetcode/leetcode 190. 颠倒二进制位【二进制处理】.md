方法一：位运算

执行用时 : 0 ms, 在Reverse Bits的C++提交中击败了100.00% 的用户

内存消耗 : 8.1 MB, 在Reverse Bits的C++提交中击败了29.04% 的用户
```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
    int i=32;
    uint32_t ans=0;
    while(i>0)
    {
        i--;
        ans<<=1;
        ans+=(n&1);
        n>>=1;
    }
        return ans;
    }
};
```

方法二：bitset  和to_ulong()配合

执行用时 : 4 ms, 在Reverse Bits的C++提交中击败了98.92% 的用户

内存消耗 : 8.2 MB, 在Reverse Bits的C++提交中击败了5.12% 的用户
```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
    bitset<32> a(n);
    for(int i=0;i<16;i++)
    {
        if(a[i]!=a[31-i])
        {
            a[i]=!a[i];
            a[31-i]=!a[31-i];
        }
    }
        
    return a.to_ulong();
    }
};
```