# 原创：leetcode 5. 最长回文子串

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        const int len = s.size();
        if(len <= 1)return s;
        int start, maxLen = 0;
        for(int i = 1; i < len; i++)
        {
            //寻找以i-1,i为中点偶数长度的回文
            int low = i-1, high = i;
            while(low >= 0 && high < len && s[low] == s[high])
            {
                low--;
                high++;
            }
            if(high - low - 1 > maxLen)
            {
                maxLen = high - low -1;
                start = low + 1;
            }
             
            //寻找以i为中心的奇数长度的回文
            low = i- 1; high = i + 1;
            while(low >= 0 && high < len && s[low] == s[high])
            {
                low--;
                high++;
            }
            if(high - low - 1 > maxLen)
            {
                maxLen = high - low -1;
                start = low + 1;
            }
        }
        return s.substr(start, maxLen);
    }
};
``` 
