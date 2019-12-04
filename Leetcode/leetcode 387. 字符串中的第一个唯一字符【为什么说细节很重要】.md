# 原创：leetcode 387. 字符串中的第一个唯一字符【为什么说细节很重要】

**执行用时 : 28 ms, 在First Unique Character in a String的C++提交中击败了98.93% 的用户**

**内存消耗 : 12.9 MB, 在First Unique Character in a String的C++提交中击败了84.31% 的用户**

![](https://img-blog.csdnimg.cn/20190601115040908.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70) 

错了两次，每次落下一个特殊条件

> 
（1）全部重复出现  
（2）没有字符


 而在题目中都是提到过的：

> 
**给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。**


 所以细心很重要。特殊情况不能忘

or（原理相同）

执行用时 : 28 ms, 在First Unique Character in a String的C++提交中击败了98.93% 的用户

内存消耗 : 13 MB, 在First Unique Character in a String的C++提交中击败了80.78% 的用户
```c++
class Solution {
public:
    int firstUniqChar(string s) {
    //计数的速度更快
    //灵活运用字符相减
    vector<int> nums(26,0);
    for(int i=0;i<s.size();i++)
    {
        nums[s[i]-'a']++;
    }
    for(int i=0;i<s.size();i++)
    {
        if(nums[s[i]-'a']==1) return i;
    }
 
        return -1;
    }
};
```

# 方法一

> 
思路：对于这种，“**最早**”类型的题，指针很好用。（时间复杂度O（n）--&gt;实际是n，也就是一遍遍历）
双指针法则：一个指当前只出现一次的位置（j），一个指当前位置（i）。
一个长度为26的临时数组，存字符出现的次数。一旦超过1就说明有重复。那j就继续跳，直到跳到不重复为止。
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        //双指针找
        //配合一个数组存是否出现过
        const int sz=s.size();
        if(sz<=0) return -1;
        int num[26]={0};
        int i=0,j=0;//双指针
        while(i<sz)
        {
            num[s[i]-'a']++;
            i++;
            while(num[s[j]-'a']>=2)
            {
                j++;
                if(j>=sz) return -1;
            }
        }
        return j;
        
    }
};
```

 

# 方法二 

unordered_map 你懂我的意思吧。

就是先存遍，再从前往后找一遍。挺快的。但是因为是map，所以可能比数组慢一些。时间复杂度也是O（n）

这个方法的好处是可以避免bug。（特殊情况很好处理。）

时间消耗：

**执行用时 : 68 ms, 在First Unique Character in a String的C++提交中击败了63.18% 的用户**

**内存消耗 : 13.2 MB, 在First Unique Character in a String的C++提交中击败了70.44% 的用户**

明显慢了很多
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> m;
        for (char c : s) m[c]++;
        for (int i = 0; i < s.size(); i++) {
            if (m[s[i]] == 1) return i;
        }
        return -1;
    }
};
```
 
