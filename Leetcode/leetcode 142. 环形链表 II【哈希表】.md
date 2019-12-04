# 原创：leetcode 142. 环形链表 II【哈希表】

方法一：无脑哈希表。

一个map数组记录访问过的结点，每次遍历时判断是否访问过。若访问过则该处即为交点。

时间复杂度：按道理是O（N），但是实际上map数组的存在使得时间复杂度变为O（N*LogN）-&gt;红黑树查找。

执行用时 :28 ms, 在所有C++提交中击败了40.08%的用户

内存消耗 :11.9 MB, 在所有C++提交中击败了7.80%的用户
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        map<ListNode *,int> m;
        //int i=0;//位置
        while(head!=NULL)
        {
            if(m[head]>0) return head;
            m[head]++;
            head=head->next;
        }
        return NULL;
    }
};
```
方法二：快慢指针找环，然后从环开始，与起点同时启动，找交点。
