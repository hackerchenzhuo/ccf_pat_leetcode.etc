# 原创：leetcode 38. 报数

题目描述有点操蛋。

> 
首先解释题目。为什么这道题是简单但差评还是这么多？我觉得问题就在于没有把题目解释清楚上。
1 读 one one
11 不读 one one one one,读 two one, 连着一起相同的数会先说数量再说值。
<p>以上是基础。接下来看怎么得到下一项的结果。从题目所给出的示例4 ： 1211 到 5 : 111221。1211 第一位是1，所以读作 one one，也就是 1 1 。2读作one two, 所以是12。 11连着读作two one, 所以是21。这所有加起来就是答案 111221。<br/>
 </p>


递归求解：
```c++
class Solution {
public:
    string fb(int k){
        if(k==1)return "1";
        else {
            string str=fb(k-1);
            string ans="";
            for(int i=0;i<str.size();){
                int j=0;
                while(j<str.size()-i){
                    if(str[i]==str[i+j]){
                        j++;
                    }
                    else break;
                }
                char c1=j+'0',c2=str[i];
                ans+=c1;ans+=c2;
                i=i+j;      
            }
            return ans;
        }
        
    }
    string countAndSay(int n) {
        return fb(n);
    }
};
```
 
