# 原创：leetcode 13.罗马数字转整数

```c++
//20.18-20.31
class Solution {
public:
    int romanToInt(string s) {
        map<char,int> m;
        m['M']=1000;m['D']=500;m['C']=100;m['L']=50;m['X']=10;m['V']=5;m['I']=1;
        
        int L=s.size();int ans=0;
        
        for(int i=0;i<L;i++){
            if(i<L-1&&m[s[i]]<m[s[i+1]]){//比后面的小，是特殊情况
                ans+=(m[s[i+1]]-m[s[i]]);
                i++;
            }
            else ans+=m[s[i]];
        }
        return ans;
    }
};
``` 
