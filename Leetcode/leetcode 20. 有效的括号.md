# 原创：leetcode 20. 有效的括号

版本1：
```c++
class Solution {//回文串问题
public:
    bool isValid(string s) {
        int L=s.size();if(L<=0) return true;
        stack<char> sta;
        map<char,char> m={{'}','{'},{')','('},{']','['}};
        for(int i=0;i<L;i++){
            if(m.find(s[i])==m.end())
            {
                //cout<<"push"<<endl;
                sta.push(s[i]);
            }
            else {
                if(sta.empty()) return false;//缺失
                else {
                char c=sta.top();sta.pop();
                if(c!=m[s[i]]){
                    //cout<<11<<endl;
                    return false;//不对应
                }
                }
            }
        }
        if(sta.empty()) return true;
        else return false;//没有弹干净
    }
};
```
版本2：
```c++
class Solution {//回文串问题
public:
    bool isValid(string s) {
        int L=s.size();if(L<=0) return true;
        stack<char> sta;
        map<char,char> m={{'}','{'},{')','('},{']','['}};
        for(int i=0;i<L;i++){
            if(m.find(s[i])==m.end())
            {
                //cout<<"push"<<endl;
                sta.push(s[i]);
            }
            else {
                char c=sta.empty()? '#' : sta.top(); 
                try
                {
                    sta.pop();
                }
                catch(...){
                    
                }
                if(c!=m[s[i]]){
                    //cout<<11<<endl;
                    return false;//不对应
                }
                }
            }
                if(sta.empty()) return true;
        else return false;//没有弹干净
        }
};
```
使用了try机制。

 

 

 
