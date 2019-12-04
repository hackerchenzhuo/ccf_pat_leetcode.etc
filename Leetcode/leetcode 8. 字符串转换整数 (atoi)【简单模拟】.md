# 原创：leetcode 8. 字符串转换整数 (atoi)【简单模拟】

一个简单模拟写了50分钟 。。错了5次。。没谁了

（1/6） 准确率16%...哎（好像正好和题目的准确率一样...）【大哥求你细心点！！！！】

**执行用时 : 8 ms, 在String to Integer (atoi)的C++提交中击败了95.34% 的用户**

**内存消耗 : 8.6 MB, 在String to Integer (atoi)的C++提交中击败了76.54% 的用户**

```c++
class Solution {
public:
    int myAtoi(string str) {
        //多种情况
        //注意正号！！！
        int sz=str.size(),i=0;
        while(i<sz&&str[i]==' ')
        {
            i++;
        }
        if(i==sz||((str[i]!='-'&&str[i]!='+')&&(str[i]>'9'||str[i]<'0'))) return 0;//空串 or 无效(非正负号开头，0-9)
        string s="";
        if(str[i]=='-') //负数
        {
            s+='-';i++;
            if(i==sz) return 0;
            if(!(str[i]<='9'&&str[i]>='0')) return 0;//无效
        }
        else if(str[i]=='+') //特殊
        {
            i++;
            if(i==sz) return 0;
            if(!(str[i]<='9'&&str[i]>='0')) return 0;//无效
        }
        int is_0=1;//是否属于前导0
        while(str[i]<='9'&&str[i]>='0'&&i<sz)
        {
            if(str[i]!='0')
            {
                s+=str[i];
                is_0=0;
                
            }
            if(str[i]=='0'&&is_0==0)
                s+=str[i];         
            i++;            
            
        }
        if(s[0]=='-'&&s.size()==1) return 0;//只有一个-
        if(s.size()==0) return 0;
        
        int max1=INT_MAX;
        int min1=INT_MIN;
        string max2,min2;
        stringstream ss;
        ss<<max1;ss>>max2;
        stringstream sss;
        sss<<min1;sss>>min2;
        if(s[0]=='-') 
        {
            if(s.size()>min2.size())
                return INT_MIN;
        }
        else if(s.size()>max2.size()) return INT_MAX;
        
        stringstream ans;
        ans<<s;
        
        long long tmp;ans>>tmp;
        
        if(tmp<INT_MIN) return INT_MIN;
        if(tmp>INT_MAX) return INT_MAX;
        
        return tmp;
        
        
    }
};
```
 

膜拜一下某位大佬的简洁版本：
```c++
class Solution {
public:
    int myAtoi(string str) {
        int i=0;
        long res=0;
        int sign=1;
        while(i<str.size() && str[i]==' ') ++i;
        if(i == str.size()) return 0;
        if(str[i]=='-') {sign=-1;i++;}
        else if(str[i]=='+') i++;          
        while(i<str.size() && isdigit(str[i]))
        {
            res=res*10+(str[i++]-'0');
            if(res>INT_MAX){
                if(sign==1) return INT_MAX;
                else return INT_MIN;
            }
        }
        return res*sign;
    }
};
//作者：li-ming-hui-2
```
 

# 相比于我的代码，他的优点：

直接用res代表了最后结果输出的一部分：// return res*sign; 

这样的好处显而易见：最主要的原因是来自于：
```c++
while(i<str.size() && isdigit(str[i]))
        {
            res=res*10+(str[i++]-'0');
            if(res>INT_MAX){
                if(sign==1) return INT_MAX;
                else return INT_MIN;
            }
        }
```
** 他在中间进行判断，而不是和我一样用stringstream完成后先用长度筛选，再用long long 赋值。及时止损，防止溢出。**

 

这样以来节省了很多事。

 

特别是这一句：
```c++
if(res>INT_MAX){
                if(sign==1) return INT_MAX;
                else return INT_MIN;
```

这个地方，用res和INT_MAX 比较。虽然**看似忽略**了一点：

> 
INT_MAX： (2^31 − 1) ；
INT_MIN ： (−2^31)；  


绝对值是不同的。所以这样的判定看似太粗糙。

**但仔细想想：当res&gt;INT_MAX的时候，是不是最小就是INT_MAX+1，也就是INT_MIN的相反数？所以这是没问题的。**

 
