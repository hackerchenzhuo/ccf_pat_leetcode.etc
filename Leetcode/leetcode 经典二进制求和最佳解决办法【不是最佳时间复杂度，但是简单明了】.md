# 原创：leetcode 经典二进制求和最佳解决办法【不是最佳时间复杂度，但是简单明了】

 
```c++
class Solution {
public:
    string addBinary(string a, string b) {
        string res = "";
        int c = 0;
        int i = a.size() - 1;
        int j = b.size() - 1;
        while(i >= 0 || j>=0 || c==1){
            c += (i>=0 ? a[i--] - '0':0);
            c += (j>=0 ? b[j--] - '0':0);
            res = char(c%2 + '0') + res;
            c /= 2;
        }
        return res;
    }
};
```