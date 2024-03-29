# 原创：leetcode 287. 寻找重复数【鸽笼原理，O（1）空间复杂度解决问题、循环列表快慢指针找环问题】

给定一个包含** n + 1 个整数的数组 nums**，其数字都在** 1 到 n 之间（包括 1 和 n）**，可知至少存在一个**重复的整数**。假设只有一个重复的整数，找出这个重复的数。

# 方法一：

**鸽笼原理**

因为在1～n的范围内最多只能放n个不同的数字，但现在数组放了n+1个数字，所以至少有一个重复。

对于在1～n范围内的某个数字m，那么数组中小于等于m的数字最少有m个，并且刚好为m的时候，**1～m之间不会有重复**，

> 
反证法：
若有重复，则必定有缺失。若有缺失，则重复数字不唯一：因为总数是n+1的。
所以不成立。无重复


 

**执行用时 :12 ms, 在所有 C++ 提交中击败了96.11%的用户**

**内存消耗 :9.9 MB, 在所有 C++ 提交中击败了27.22%的用户**
```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int low = 1, high = nums.size()-1;
        while (low<high) {
            int mid = (low+high)/2;
            int count = 0;
            for(int num: nums) if (num<=mid) count++;
            if (count > mid) high = mid;//重复的出现在在前面
            else low = mid + 1;//前面的无重复，重复的出现在后面
        }
        return low;
    }
};
```

# 方法二：

**循环列表快慢指针判断：**

注意：数字都在** 1 到 n 之间（包括 1 和 n）**

**所以 参考【[here](https://blog.csdn.net/jmspan/article/details/51158516)】**
![](https://img-blog.csdn.net/20160415091505120?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

> 
快慢指针追击问题。
第一次相交确定有环。然后slow指针继续移动，并且设置第二个slow指针从起点正向移动（or当前位置反向移动），交点即为入环的位置。


 **注意：快慢指针要用do while起手。减少代码量**

> 
**执行用时 :12 ms, 在所有 C++ 提交中击败了96.11%的用户**
**内存消耗 :9.9 MB, 在所有 C++ 提交中击败了34.65%的用户**
```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
int slow = 0, fast = 0;
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (nums[slow] != nums[fast]);
        int restart = 0;
        while (nums[restart] != nums[slow]) {
            restart = nums[restart];
            slow = nums[slow];
        }
        return nums[restart];
    }
};
```

 
