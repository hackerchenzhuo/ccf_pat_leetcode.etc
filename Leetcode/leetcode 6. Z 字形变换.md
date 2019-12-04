# 原创：leetcode 6. Z 字形变换

最快的方法就是跟踪Z的形状

碰到可以 mod 的地方（边界处），**就转向**。时间复杂度，具体点说是O（2n）。【相当于遍历了两次】。

特殊情况：维度等于1的时候，拿出来单独考虑。

**执行用时 : 28 ms, 在ZigZag Conversion的C++提交中击败了74.08% 的用户**

**内存消耗 : 14.3 MB, 在ZigZag Conversion的C++提交中击败了75.08% 的用户**
```c++
class Solution {
public:
    string convert(string s, int numRows) {
        //跟踪z的型状即可
        int sz=s.size();
        if(sz<=2||numRows==1) return s;
        int add=-1;
        vector<char> ans[numRows];
        for(int i=0,j=0;i<sz;i++)
        {
            if(j%(numRows-1)==0) add=-add;//转向
            ans[j].push_back(s[i]);
            j+=add;
        }
        string res="";
        for(int i=0;i<numRows;i++)
        {
            for(int j=0;j<ans[i].size();j++)
            {
                res+=ans[i][j];
            }
        }
        return res;
    }
};
```

更快的方法是像官网解读的那样：
![](https://img-blog.csdnimg.cn/20190602220142917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

**这个的时间复杂度是O（n），可以快一倍。但是数量级依然相同。**

 

因为比较懒，所以就不考虑了。
