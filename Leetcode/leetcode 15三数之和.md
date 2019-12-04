# 原创：leetcode 15三数之和

最开始的想法很简单，双指针遍历，查询，时间复杂度O（n^3），过不了最后几个案例。
![](https://img-blog.csdnimg.cn/20190501112202686.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
      vector<vector<int>> kong;
        vector<vector<int>> test;
    if(nums.size()<=2) {       
            return kong;  
    }
    else{
        for(int i=0;i<nums.size()-1;i++){
            for(int j=i+1;j<nums.size();j++){
                int need=0-nums[i]-nums[j];
                auto it=find(nums.begin()+j+1,nums.end(),need);//防重复，这样能保证不出现重复  统计
                if(it!=nums.end()){
                    //if(it-nums.begin()>j)
                    {
                    int f=*it;
                    vector<int> key(3);key[0]=nums[i];key[1]=nums[j];key[2]=f;
                    sort(key.begin(),key.end());
                    if(find(kong.begin(),kong.end(),key)==kong.end()){//这样能保证不出现重复  组合
                        kong.push_back(key);
                    }
                    }
 
                }
            }
        }
    }
        return kong;
    }
};
```

 估摸着，空间换时间————用hash存元素，然后进行遍历。

时间复杂度：

1.遍历vector——n。

2.双指针遍历数组——n^2.  hash:log2n（红黑树查找）

-&gt;n+n^2*logn=O（n^2*logn）

可以一试；
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
    //sort(nums.begin(),nums.end());
    vector<vector<int>> kong;
    
    if(nums.size()<=2) {       
        return kong;  
    }
    else{
        
        map<int,int> tmp;//索引数组
        auto it=nums.begin();  
        it=nums.begin();
        while(it!=nums.end()){//遍历
            tmp[(*it)]+=1;//默认是排序的
            it++;
        } 
        int max=(--tmp.end())->first;//最大正数
        for(auto itm=tmp.begin();itm!=tmp.end();itm++){
            if(itm->first>0) break;//提前结束
            itm->second--;
            for(auto jtm=itm;jtm!=tmp.end();jtm++){
                    int kk=itm->first+jtm->first;
                    if(kk>0){
                        break;//后面的不可能比前面的小了
                    }
                    else if((-1)*kk>max){
                        continue;
                    }
                    if(jtm->second>0)
                    {
                    jtm->second--;
                    int need=0-kk;
                    if(need>=jtm->first&&tmp[need]>0){
                        vector<int> k={itm->first,jtm->first,need};
                         kong.push_back(k);
                    }
                    jtm->second++;
                    }
                    
                }
            itm->second++;
            }
        }  
        return kong;
    }
};
```

万万没想到还是超时。惨绝人寰，丧心病狂！！！！！

 

最后看了一下标准解法：

1.排序。

2.定位一个，然后用类似快排的手法，两边往中间移动，加上适当剪枝。一次可以检索出一个数字对应的所有情况。

剪枝：

> 
<p>if (nums[i] &gt; 0){<br/>
                break;<br/>
            }<br/>
            if (i &gt; 0 &amp;&amp; nums[i] == nums[i-1]){<br/>
                continue;<br/>
            }</p>


时间复杂度等于是：

排序：n*log2(n)

内部：n*n（类似于两遍遍历数组），一次可以找出一对。比一个个找快多了。

总的时间复杂度  O（n^2）

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
       // int i = 0, left = 0, right = 0,tar = 0;
        sort(nums.begin(),nums.end());
        for (int i = 0; i < nums.size(); ++i){
            if (nums[i] > 0){
                break;
            }
            if (i > 0 && nums[i] == nums[i-1]){
                continue;
            }
            int left = i + 1;
            int right = nums.size() - 1;
            int tar = - nums[i];
            while (left < right) {
                if( nums[left] + nums[right] == tar){
                    res.push_back({nums[i],nums[left],nums[right]});
                    while (nums[left + 1] == nums[left] && left < right){
                        ++ left;
                    }
                    while (nums[right - 1] == nums[right] && right > left){
                        --right;
                    }
                  //  ++ left;
                    -- right;
                } else if (nums[left] + nums[right] > tar){
                    --right;
                } else{
                    ++left;
                }
            }
        }
        return res;
    }
};
```


 
