# 原创：leetcode 139. 单词拆分【记忆化搜索法进行回溯剪枝】

> 
方法一：
暴力dfs+回溯
<p>时间复杂度：O(n^n)。考虑最坏情况 ss =aaaaaaa 。每一个前缀都在字典中，此时回溯树的复杂度会达到 n^n<br/>
空间复杂度：O(n)O(n) 。回溯树的深度最深达到 nn 。</p>


果不其然超时了

![](https://img-blog.csdnimg.cn/20190610191959934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        //字典无重复词
        sort(wordDict.begin(),wordDict.end());//从小到大排序
        //reverse(wordDict.begin(),wordDict.end());//逆序
        return find(s,0,wordDict);
    }
    
    bool find(string &s,int sta,vector<string>& wordDict)//查找函数
    {
        if(sta==s.size()) return true;
        for(int i=0;i<wordDict.size();i++)
        {
            if(comp(s,sta,wordDict[i]))
            {
                bool ok=find(s,sta+wordDict[i].size(),wordDict);
                if(ok) return true;//到终点完全匹配了
                //否则继续（回溯）
            }  
        }
        return false;//没找到
    }
    bool comp(string &s,int &sta,string &word)//比较函数
    {
        if(s.size()-sta<word.size()) return false;//此时剩余的长度还不到word的长度
        for(int i=0;i<word.size();i++)
        {
            if(s[sta+i]!=word[i]) return false;
        }
        return true;
    }
};
```
 改进：

因为有重复过程，所以用**记忆化搜索法进行回溯剪枝**

在先前的方法中，我们看到许多函数调用都是冗余的，也就是我们会对相同的字符串调用多次回溯函数。为了避免这种情况，我们可以使用记忆化的方法，其中一个 数组用来保存子问题的结果。每当访问到已经访问过的后缀串，直接用 memo数组中的值返回而不需要继续调用函数。

 

**执行用时 :4 ms, 在所有C++提交中击败了99.52%的用户**

**内存消耗 :8.7 MB, 在所有C++提交中击败了96.07%的用户**

**核心：**

> 
vector&lt;int&gt; tag(s.size()+5,-1);


 ●加5是为了防止出现什么边界错误（还真出现了。。。想不通）

 ●主要就是维护一个长度和s相同的数组，初值为-1。

 ●每个下标代表从对应位置处开始能否得到最终的匹配结果。

 ●因为存在重复调用的可能，所以：

> 
**1.一旦判断完该位置不可行，就要置0，下次继续到这直接跳过；**
**2.一旦判断该位置可行就置1，下次直接返回true**

```c++
class Solution {
public:
    
    bool wordBreak(string s, vector<string>& wordDict) {
        //字典无重复词
        vector<int> tag(s.size()+5,-1);
        sort(wordDict.begin(),wordDict.end());//从小到大排序
        //reverse(wordDict.begin(),wordDict.end());//逆序
        return find(s,0,wordDict,tag);
    }
    
    bool find(string &s,int sta,vector<string>& wordDict,vector<int> &tag)//查找函数
    {
        if(tag[sta]>0||sta==s.size()) return true;//该处搜索过
        if(tag[sta]==0) return false;
        for(int i=0;i<wordDict.size();i++)
        {
            if(comp(s,sta,wordDict[i]))
            {
                bool ok=find(s,sta+wordDict[i].size(),wordDict,tag);
                if(ok) 
                {
                    tag[sta]=1;
                    return true;//到终点完全匹配了
                }
                //否则继续（回溯）
                else tag[sta]=0;
            }  
        }
        return false;//没找到
    }
    bool comp(string &s,int &sta,string &word)//比较函数
    {
        if(s.size()-sta<word.size()) return false;//此时剩余的长度还不到word的长度
        for(int i=0;i<word.size();i++)
        {
            if(s[sta+i]!=word[i]) return false;
        }
        return true;
    }
};
```
 
