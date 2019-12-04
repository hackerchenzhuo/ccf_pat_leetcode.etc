# 原创：leetcode 202. 快乐数【循环相关！快慢指针】

**一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。**

 

> 
<pre>
**输入:** 19
**输出:** true
<strong>解释: 
</strong>12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1 </pre>


题解：

解法一：先验！

不快乐数必定陷入：**4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4**的循环中

所以只要是不快乐数，一定出现4！

章口就来：

执行用时 : 0 ms, 在Happy Number的C++提交中击败了100.00% 的用户

内存消耗 : 8.1 MB, 在Happy Number的C++提交中击败了74.61% 的用户
```c++
class Solution {
public:
    bool isHappy(int n) {
        int ans=n;
        while(ans!=1)
        {
            n=ans;
            ans=0;
            while(n>0)
            {
                ans+=pow((n%10),2);
                n/=10;
            }
            if(ans==4) return false;
        }
        return true;
    }
};
```

方法二：

来点又技术含量的，快慢指针！

**快指针 言：“慢先生，这世间所有的相遇都是久别重逢”**

执行用时 : 4 ms, 在Happy Number的C++提交中击败了99.27% 的用户

内存消耗 : 8.3 MB, 在Happy Number的C++提交中击败了51.77% 的用户
```c++
class Solution {
public:
    bool isHappy(int n) {
        int a=n,b=n;
        while(a!=1&&b!=1)
        {
            a=findnext(a);
            b=findnext(findnext(b));
            if(a==b&&a!=1) return false; 
        }
        return true;
    }
    int findnext(int n)
    {
        int ans=0;
        while(n>0)
        {
            ans+=pow((n%10),2);
            n/=10;
        }
        return ans;
    }
};
```
 

 

 
