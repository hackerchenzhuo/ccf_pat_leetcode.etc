# 原创：leetcode 242. 有效的字母异位词【哈希表】

执行用时 : 12 ms, 在Valid Anagram的C++提交中击败了96.97% 的用户

内存消耗 : 9.5 MB, 在Valid Anagram的C++提交中击败了10.79% 的用户

easy

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size()!=t.size()) return false;
        int ans[26]={0};
        int sz=s.size();
        for(int i=0;i<sz;i++)
        {
            ans[s[i]-'a']++;
            ans[t[i]-'a']--;
        }
        for(int i=0;i<26;i++)
        {
            if(ans[i]!=0) return false;
        }
        return true;
    }
};
``` 
