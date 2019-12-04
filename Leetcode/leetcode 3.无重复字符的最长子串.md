# 原创：leetcode 3.无重复字符的最长子串

![](https://img-blog.csdnimg.cn/20190423202621571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 我的代码：

缺点：暴力搜索，太慢了。最终击败5%的人。。。

 ```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int L=s.size();
        if(L<=1) return L;
        map<char,int> m;
        int max=1;
        for(int i=0;i<L-max+1;i++)
        {
            int t=0;
            for(int j=i;j<L;j++)
            {
                if(!m[s[j]]) {
                    m[s[j]]=1;
                    t++;
                    if(t>max) max=t;
                }
                else break;
            }
            m.clear();
        }
        return max;
        
        
    }
};
```

看了解析：用哈希表做（保存出现过的位置）

然后滑动窗口分两种情况讨论。

最终击败百分之99.6%的人

 
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int map[257]={0};
        int left=0;
        int max=0;
        int t=0;
        int i;
        for(i=0;i<s.size();i++){
            if(map[s[i]]==1){
                t=i-left;
                    if(t>max) max=t;
                t=0;
                while(s[left]!=s[i]){
                    map[s[left]]=0;
                    left++;
                }
                left++;
                
            }
            map[s[i]]=1;
            
            
        }
         t=i-left;
         if(t>max) max=t;
        return max;
    }
        
};
```