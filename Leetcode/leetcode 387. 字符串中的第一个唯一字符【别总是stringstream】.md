# 原创：leetcode 387. 字符串中的第一个唯一字符【别总是stringstream】

**stringstream很慢的，能不用就不用**

使用**stringstream：**

执行用时 : 28 ms, 在First Unique Character in a String的C++提交中击败了98.93% 的用户

内存消耗 : 13 MB, 在First Unique Character in a String的C++提交中击败了80.78% 的用户
```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        //15,5,3
        vector<string> ans;
        for(int i=1;i<=n;i++)
        {
            if(i%15==0) ans.push_back("FizzBuzz");
            else if(i%5==0) ans.push_back("Buzz");
            else if(i%3==0) ans.push_back("Fizz");
            else  
            {
                stringstream ss;ss<<i;
                string b;ss>>b;
                ans.push_back(b);
            }
        }
        return ans;
    }
};
```
 

 不用**stringstream**：

执行用时 : 12 ms, 在Fizz Buzz的C++提交中击败了94.06% 的用户

内存消耗 : 10.3 MB, 在Fizz Buzz的C++提交中击败了57.14% 的用户

**改了一句话，快了一倍。**

```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        //15,5,3
        vector<string> ans;
        for(int i=1;i<=n;i++)
        {
            if(i%15==0) ans.push_back("FizzBuzz");
            else if(i%5==0) ans.push_back("Buzz");
            else if(i%3==0) ans.push_back("Fizz");
            else  
               ans.push_back(to_string(i));
 
        }
        return ans;
    }
};
``` 
