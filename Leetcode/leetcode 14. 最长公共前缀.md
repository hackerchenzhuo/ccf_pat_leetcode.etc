# 原创：leetcode 14. 最长公共前缀

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int len=0;int flag=1;
        int Size=strs.size();
        if(Size==0) return "";
        if(Size==1) return strs[0];
        int L=strs[0].size();//最长不超过这个
       
        while(1){
        int i=1;
        if(len>L) break;//不可能了
        for(;i<Size;i++){
            if(len>=strs[i].size()||strs[i][len]!=strs[0][len]) {flag=0;return strs[0].substr(0,len);}
            //超过了某一个字串的长度or和第一个str不匹配了
    
        }
        len++;
        } return "123";
        
        
        
    }
};
``` 
