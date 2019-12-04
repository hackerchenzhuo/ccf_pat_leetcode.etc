# 原创：leetcode 58. 最后一个单词的长度

 
```c++
class Solution {
public:
    int lengthOfLastWord(string s) {
        stringstream ss;
        ss<<s;
        string t="";
        ss>>t;
        if(t==""||t==" ") return 0;
        string ans=t;
        while(ss>>t){
            ans=t;
        }
        return ans.size();
        
    }
};
```
