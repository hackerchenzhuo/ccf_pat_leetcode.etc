# 原创：leetcode 438. 找到字符串中所有字母异位词【傻子才用全排列（比如我）】

remember:

时间使用增加原因：

1.函数传入的参数比较复杂，每一次的拷贝很耗时间

2.能用下标表示的用下标。尽量抽象

参考[leetcode 242. 有效的字母异位词【哈希表】](https://chenzhuo.blog.csdn.net/article/details/90714165)

最开始的想法：

> 
<p>    //用map<br/>
    //在全排列中检索。<br/>
    //因为有红黑树，所以时间复杂度O（2lgn+n），还好<br/>
    //visit数组记录是否访问过,level定义当前到哪了</p>

```c++
class Solution {
public:
    //用map
    //在全排列中检索。
    //因为有红黑树，所以时间复杂度O（2lgn+n），还好
    //visit数组记录是否访问过,level定义当前到哪了
    map<string,int> m;
    void dfs(string s,int level,vector<int> &visited,string now="")//找全排列
    {
        if(level>=s.size()){//满了
            //cout<<now<<endl;
            if(m[now]!=1)
                m[now]=1;
            return;
        }
        for(int i=0;i<s.size();i++){
            if(visited[i]==1) continue;
            visited[i]=1;
            string t=now;
            t=t+s[i];
            
            dfs(s,level+1,visited,t);
            visited[i]=0;
        }
        
    }
    vector<int> findAnagrams(string s, string p) {
        
        vector<int> ans;
        if(s.size()<p.size()) return ans;
        vector<int>vis(p.size(),0);
        int sz=s.size();
        dfs(p,0,vis);
        for(int i=0;i<=sz-p.size();i++)
        {
            //cout<<s.substr(i,p.size())<<endl;
            if(m[s.substr(i,p.size())]==1)
            {
                ans.push_back(i);
            }
        }
        return ans;
        
        
        
    }
};
```

 

> 
万万没想到，时间炸了
其实不炸是不可能的，求全排列算法的时间复杂度可不是闹着玩，O(n！)。。。伤不起。


最佳方法：

记录每个字符（26个）出现的次数，然后依次对比。

> 
最基本思路是，用哈希表记录p串中每个字母的出现次数，在串s每个允许的子串上判断每个字母的出现次数一不一样就可以了。
可以这样去优化一下“判断字母出现次数一不一样”，即每次遇到一个字母，就在哈希表里把这个字母出现次数-1，这样当所有字母变化到（注意，有可能是“减小到”也有可能是“增加到”）0的时候就是匹配成功了。
而当索引i在串s上移动超过串p的长度plen时，每次往后移动一个，都要把这个子串的开头的前一个字母记录回来，这里也就是在哈希表中将该字母出现次数+1。


执行用时 : 156 ms, 在Find All Anagrams in a String的C++提交中击败了22.36% 的用户

内存消耗 : 285.4 MB, 在Find All Anagrams in a String的C++提交中击败了5.23% 的用户

 

好歹是通过了。。。 

```c++
class Solution {
public:
    //统计各字母出现的次数即可
    //存储空间可以共用
    map<int,int> m;
    bool jug(string s,map<int,int> &m,char k=' ')
    {
        int flag=0;
        if(k==' ')
        {
         for(int i=0;i<s.size();i++)
        {
            if(m[s[i]-'a']==0) flag=1;
            m[s[i]-'a']--;
        }
        }
        else
        {
            m[k-'a']++;
            if(m[s[s.size()-1]-'a']==0)
            {
                 flag=1;
            }
            m[s[s.size()-1]-'a']--;
        }
 
        if(flag) return false;
        for(auto it=m.begin();it!=m.end();it++)
        {
            if(it->second!=0) return false;
        }
        return true;
        
    }
    vector<int> findAnagrams(string s, string p) {
        vector<int> ans;
        if(s.size()<p.size()) return ans;
        map<int,int> m;
        for(int i=0;i<26;i++)
        {
            m[i]=0;
        }
        for(int i=0;i<p.size();i++)
        {
            m[p[i]-'a']++;
        }
        
          if(jug(s.substr(0,p.size()),m))
            {
                ans.push_back(0);
            }
        for(int i=1;i<=s.size()-p.size();i++)
        {
            if(jug(s.substr(i,p.size()),m,s[i-1]))
            {
                ans.push_back(i);
            }
        }
        return ans;
        
        
        
    }
};
```

 优化：

每当一个字母数量减少或者增加到0，将其记录一下；每当一个字母从0减少或增加成其它数字，也记录一下。这两件事用一个变量（代码中的nz，寓意not zero）记录就可以了。

我的代码：

别人家的代码。。。。

**【对于全0数组的判断可以直接与实现设定好的vector数组用（==）对比。涨知识了！！！！】**

执行用时 : 44 ms, 在Find All Anagrams in a String的C++提交中击败了94.20% 的用户

内存消耗 : 10.3 MB, 在Find All Anagrams in a String的C++提交中击败了72.09% 的用户

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        if(p.size()>s.size()){
            return {};
        }
        vector<int> res;
        vector<int> vs(26,0);
        vector<int> vp(26,0);
        int start = 0;
        for(int i = 0;i < p.size();i++){
            vs[s[i]-'a']++;
            vp[p[i]-'a']++;
        }
        if(vs==vp){
            res.push_back(start);
        }
        for(int i = p.size() ;i < s.size();i++){
            vs[s[start]-'a']--;
            vs[s[i]-'a']++;
            start++;
            if(vs==vp){
                res.push_back(start);
            }
        }
        return res;
    }
};
``` 
