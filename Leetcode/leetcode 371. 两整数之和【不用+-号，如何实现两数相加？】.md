# 原创：leetcode 371. 两整数之和【不用+-号，如何实现两数相加？】

**两个整数a, b; a ^ b是无进位的相加； a&amp;b得到每一位的进位；让无进位相加的结果与进位不断的异或， 直到进位为0；**

```c++
class Solution {
public:
    int getSum(int a, int b) {
        while (a & b) {
            int n = a;
            int m = b;
            a = n ^ m;
            b = (unsigned int)(n & m) << 1;
        }
        return a ^ b;
    }
};
``` 
