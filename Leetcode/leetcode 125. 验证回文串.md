# 原创：leetcode 125. 验证回文串

执行用时 : 8 ms, 在Valid Palindrome的C++提交中击败了99.47% 的用户

内存消耗 : 9.6 MB, 在Valid Palindrome的C++提交中击败了8.01% 的用户

两遍遍历：
```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int cha='a'-'A';
        string k="";
        for(int i=0;i<s.size();i++)
        {
            if(s[i]>='a'&&s[i]<='z'||s[i]>='0'&&s[i]<='9')
            {
                k+=s[i];
            }
            else if(s[i]>='A'&&s[i]<='Z')
            {
                s[i]+=cha;
                k+=s[i];
            }  
        }
        
        for(int i=0;i<k.size()/2;i++)
        {
            if(k[i]!=k[k.size()-1-i]) return false;
        }
        return true;
    }
};
```

更好的方法：

一遍遍历——双指针，遍历的过程遇到非数字和字母则跳过！！！！这样只需要一遍遍历
```c++
class Solution {
public:
   bool isPalindrome(string s) {
         int left = 0, right = s.size() - 1 ;
         while (left < right) {
             if (!isAlphaNum(s[left])) ++left;
             else if (!isAlphaNum(s[right])) --right;
             else if ((s[left] + 32 - 'a') %32 != (s[right] + 32 - 'a') % 32) return false;
             else {
                 ++left; --right;
             }
         }
         return true;
     }
     bool isAlphaNum(char &ch) {
         if (ch >= 'a' && ch <= 'z') return true;
         if (ch >= 'A' && ch <= 'Z') return true;
         if (ch >= '0' && ch <= '9') return true;
         return false;
     }
};
```
 
