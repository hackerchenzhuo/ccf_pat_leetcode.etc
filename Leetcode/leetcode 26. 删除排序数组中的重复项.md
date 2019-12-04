# 原创：leetcode 26. 删除排序数组中的重复项

本来以为自己的代码很简洁，效率很高，但是忘记了，在不使用迭代器的话，每次寻址都是按链表从头遍历，导致效率惨不忍睹。

（本来最开始想的是用空间换时间。）

上代码一：
```c++
//21.05
class Solution {
    //easy
    //空间换时间的典型代表。
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1) return nums.size();
        else{
            //vector<int>::iterator it=nums.begin();
            int i=0;
            int now=nums[0];
            i++;//防野指针
            while((nums.begin()+i)!=nums.end()){
                if(*(nums.begin()+i)==now){
                    nums.erase(nums.begin()+i);
                }
                else {
                    now=*(nums.begin()+i);
                    i++;
                    }
            }
        }
        return nums.size();
    }
};
```

 用时：
![](https://img-blog.csdnimg.cn/20190427212109176.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 

代码二：

用迭代器试试：
```c++
//21.05
class Solution {
    //easy
    //空间换时间的典型代表。
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1) return nums.size();
        else{
            vector<int>::iterator it=nums.begin();
            it++;
            //int i=0;
            int now=nums[0];
            //i++;//防野指针
            while((it)!=nums.end()){
                if(*(it)==now){
                    nums.erase(it);
                }
                else {
                    now=*it;
                    it++;
                    }
            }
        }
        return nums.size();
    }
};
```

我是万万没想到，换了迭代器还这么慢？？？？（好心人能解释一下吗）

 ![](https://img-blog.csdnimg.cn/20190427212547459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

方法三：空间换时间：
```c++
//21.05
class Solution {
    //easy
    //空间换时间的典型代表。
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1) return nums.size();
        else{
            //建立空间数组
            const int max=*(nums.end()-1);
            const int min=*nums.begin();//防止负数情况
            int m[max-min+1]={0};
            for(int i=0;i<nums.size();i++){
                m[nums[i]-min]=1;
            }
            vector<int> ans;
            for(int i=0;i<=max-min;i++){
                if(m[i]) ans.push_back(i+min);
            }
            nums=ans;
        }
        return nums.size();
    }
};
```
![](https://img-blog.csdnimg.cn/20190427213519848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
结果稍微有好转。但是还是很低。

 

### **标准解法：**
![](https://img-blog.csdnimg.cn/20190427213825462.png)
 

没有删除操作，没有插入操作，只有赋值操作。因此速度自然快了。

java代码：
```c++
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```
 
