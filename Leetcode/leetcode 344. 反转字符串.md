# 原创：leetcode 344. 反转字符串

执行用时 : 64 ms, 在Reverse String的C++提交中击败了96.16% 的用户

内存消耗 : 15.2 MB, 在Reverse String的C++提交中击败了76.27% 的用户

eeeee

=============================================================================================

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        reverse(s.begin(),s.end());
    }
};
``` 

其实可以双指针迭代。一个前一个后。总之挺简单的。
