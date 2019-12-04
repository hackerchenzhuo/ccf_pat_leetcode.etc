# 原创：leetcode 208. 实现 Trie (前缀树)【多叉树，前缀匹配】【代码很精炼】

说到前缀，说到树，自然想到set。set内部是红黑树，有自动排序二分查找的功能，查找时间复杂度可以降低到logn。但是。。。一个个录入会导致效率奇低，查找开销也大

# 方法一：

双set，一个存前缀，一个存全匹配。。额这效率

**执行用时 :552 ms, 在所有 C++ 提交中击败了5.21%的用户**

**内存消耗 :112.9 MB, 在所有 C++ 提交中击败了5.14%的用户**

```c++
class Trie {
public:
    set<string> fron;//前缀树
    set<string> allmatch;//全匹配
    /** Initialize your data structure here. */
    Trie() {//两个set解决问题
        
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        allmatch.insert(word);
        int sz=word.size();
        for(int i=1;i<=sz;i++)
        {
            fron.insert(word.substr(0,i));
        }
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        if(allmatch.find(word)!=allmatch.end())
        {
            return true;
        }
        return false;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        if(fron.find(prefix)!=fron.end())
        {
            return true;
        }
        return false;
    }
};
 
/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
 ```

# 方法二：结合背景看看别人的方法：

> 
Trie树，即字典树，又称单词查找树或键树，是一种树形结构，是一种哈希树的变种。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。
<p>    Trie的核心思想是空间换时间。利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。 <br/>
它有3个基本性质：</p>
<ol>- 根节点不包含字符，除根节点外每一个节点都只包含一个字符。
- 从根节点到某一节点，路径上经过的字符连接起来，为该节点对应的字符串。
- 每个节点的所有子节点包含的字符都不相同。
</ol>
![](https://images0.cnblogs.com/blog/440499/201308/05224451-13131c79f51b4fbbb0c5e882d3a50927.jpg)
 

 使用前缀树，总共的结点，空间不会超过：单词数量*单词长度。假设是1000个词，长度为10 ，那么空间不超过10000 O（n*m）

用双set法，虽然set可以去重复，但是保守估计空间也需要55*1000=55000  O（n*m^2）

同时，时间复杂度的话也会上升。

> 
**执行用时 :88 ms, 在所有 C++ 提交中击败了94.99%的用户**
**内存消耗 :45 MB, 在所有 C++ 提交中击败了32.71%的用户**


 上代码：【代码很精炼，值得学习】

**1.用is_str判断一个单词是否读入结束【实现相同前缀情况下的空间复用存储】**

**2.递归new前缀树，数据结构元素均可复用。**

**3.前缀搜索时不需要判断is_str，全匹配完了就行。完全搜索时需要判断is_str且非空。**
```c++
 
class Trie {
public:
    bool is_str; // 标识当前结点是否为一个完整的字符串
    Trie *next[26]; // 下一个结点的指针数组
    Trie() {
        is_str = NULL;
        memset(next,0,sizeof(next));
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        Trie *cur = this; // cur初始化为根结点指针
        for(char w : word){ // 遍历word中的每一个字符
            if(cur->next[w-'a']==NULL){ // 下一个结点不存在，新增一个结点
                Trie *new_node = new Trie();
                cur->next[w-'a'] = new_node;
            }
            cur = cur->next[w-'a'];
        }
        cur->is_str = true; // 当前结点已经是一个完整的字符串了
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Trie *cur = this;
        for(char w : word){
            if(cur!=NULL)
                cur = cur->next[w-'a']; // 更新cur指针的指向，使其指向下一个结点
        }
        return (cur!=NULL&&cur->is_str); // cur指针不为空且cur指针指向的结点为一个完整的字符串，则成功找到字符串
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
         Trie *cur = this;
        for(char w : prefix){
            if(cur!=NULL)
                cur = cur->next[w-'a'];
        }
        return (cur!=NULL); // 相比search(),这里只需判断cur指针是否为空就行了
    }
};
```
![](https://img-blog.csdnimg.cn/20190617224247110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 

### 结果显而易见。后两次是前缀树，前两次是set。差别巨大。 
