# 原创：LeetCode 309. 最佳买卖股票时机含冷冻期:【一个很清晰的动态规划解题思路，状态机教程】

**执行用时 :0 ms, 在所有 C++ 提交中击败了100.00%的用户**

**内存消耗 :8.9 MB, 在所有 C++ 提交中击败了73.55%的用户**

# 问题来源

<br/>
题目来源链接见下方： <br/>
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/

# 问题简述：

<br/>**假如有一个 i 个元素的数组，数组的每个元素表示了第 i 天某只股票的价格，设计一种算法来找到利润最大的买卖方式。设计的算法必须遵守以下两条约束条件：**

<strong>在一天当中，只能进行“买”，“卖”或者“什么都不干”中的一种操作<br/>
在“卖”掉股票之后，必须“什么都不干”一天<br/>
举个例子：</strong>

> 
<p>prices = [1, 2, 3, 0, 2]<br/>
maxProfit = 3<br/>
transactions = [buy, sell, cooldown, buy, sell]</p>


# <br/>
解题思路

<br/>
首先申明一下，这个思路并不是我想出来的，只是在LeetCode上看到有人这样解，觉得这个思路很不错，所以写下来作为分享和记录。 <br/>
从题目中可以看出，不管哪一天，都只能是 buy 或者 sell 或者 cooldown(rest) 三种状态中的一种，而根据题目的约束条件，我们可以画出下图所示的状态图： <br/>

![](https://img-blog.csdn.net/20170731204512323?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvemp1UGVjbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 

由此图我们可以得到：

 其中s0，s1，s2分别表示三种状态下的最大利润值。 <br/>
值得注意的是这里的s0，s1和s2不是单纯的buy，sell， rest，而应该是

 

同时，可以注意到的是，每次的状态 i 都只与前一次的状态 i - 1有关，也就是说我们可以把空间复杂度从O(n)降到O(1)。

# 解题代码

好了，话不多说，下面是时间复杂度为O(n)，空间复杂度为O(1)的DP代码：

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.size() <= 1)
            return 0;
        int s0 = 0;
        int s1 = -prices[0];
        int s2 = INT_MIN;
        for (int i = 1; i < prices.size(); i++){
            int pre0 = s0;
            int pre1 = s1;
            int pre2 = s2;
            s0 = max(pre0, pre2);
            s1 = max(pre0 - prices[i], pre1);
            s2 = pre1 + prices[i];
        }
        //最大利润不可能出现在buy而未sell的时候，所以不考虑s1
        return max(s0, s2);
    }
};
``` 

 
