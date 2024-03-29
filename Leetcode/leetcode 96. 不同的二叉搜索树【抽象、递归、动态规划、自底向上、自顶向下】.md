# 原创：leetcode 96. 不同的二叉搜索树【抽象、递归、动态规划、自底向上、自顶向下】

 

**执行用时 : 4 ms, 在Unique Binary Search Trees的C++提交中击败了93.54%的用户**

**内存消耗 : 8.3 MB, 在Unique Binary Search Trees的C++提交中击败了11.31% 的用户**

 

## 解法一：自顶向下

用递归和动态规划的方法，找不同的情况。

一般这种题是不能真的模拟二叉树构建的，那样子太耗时间了。需要抽象出来流程。

 

找不同的二叉树可以划分为子问题，左边和右边情况，左边要保证小于中间，右边要保证大于中间。而且由于是二叉搜索树，所以**中间那个结点位置是固定的**，不是谁都可以想来就来。

左右分开子问题讨论。**使用自顶向下的过程。**

 

为了避免重复计算，使用动态规划的打表方法，记录每种情况下有多少种可能的结果。
```c++
class Solution {
public:
    
    int numTrees(int n) {
        //二叉搜索树：以一个结点为根，其他结点为左右子树,左边的小于根，右边的大于根
        //动态规划问题
        //最终的数量等于 左边的数量*右边的数量
        if(n<=1) return 1;
        vector<int> t(n+1,0);
        t[0]=t[1]=1;
        return nums(n,t);
    }
    int nums(int n,vector<int> &t)
    {
        if(t[n]>0) return t[n];
        int ans=0;
        for(int i=0;i<n;i++)
        {
            ans+= nums(i,t)*nums(n-1-i,t);
        }
        t[n]=ans;
        return ans;
    }
};
```
 

## 解法二：自底向上

**PS：发现自己真的很喜欢用递归....**

### **骚年，要克制对递归的依赖呀！！！！！**

正宗动态规划：

**因为递归会让空间占用大大增加，所以尽量少用递归。**

看了一下解析，发现自己所做的方法名字叫：

> 
<p>假设n个节点存在二叉排序树的个数是G(n)，令f(i)为以i为根的二叉搜索树的个数，则<br/>
G(n) = f(1) + f(2) + f(3) + f(4) + ... + f(n)G(n)=f(1)+f(2)+f(3)+f(4)+...+f(n)</p>
<p>当i为根节点时，其左子树节点个数为i-1个，右子树节点为n-i，则<br/>
f(i) = G(i-1)*G(n-i)f(i)=G(i−1)∗G(n−i)</p>
**综合两个公式可以得到卡特兰数公式**<br/>**G(n) = G(0)*G(n-1)+G(1)*(n-2)+...+G(n-1)*G(0)**


**执行用时 : 4 ms, 在Unique Binary Search Trees的C++提交中击败了93.54%的用户**

**内存消耗 : 8.2 MB, 在Unique Binary Search Trees的C++提交中击败了58.16% 的用户**

### **不使用递归可以大大减少空间消耗**
```c++
class Solution {
public:
    int numTrees(int n) {
        //二叉搜索树：以一个结点为根，其他结点为左右子树,左边的小于根，右边的大于根
        //动态规划问题
        //最终的数量等于 左边的数量*右边的数量
        int dp[n+1]={0};
        dp[0]=dp[1]=1;
        for(int i=2;i<n+1;i++)//自底向上，从2一直到n
        {
            for(int j=0;j<i;j++)
            {
                dp[i]+=dp[j]*dp[i-j-1];
            }
        }
        return dp[n];
    }
};
```
代码也简洁了很多！！！！

 
