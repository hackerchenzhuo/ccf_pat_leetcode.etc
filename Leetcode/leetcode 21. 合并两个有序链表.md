# 原创：leetcode 21. 合并两个有序链表

主要就是先把两个链表读出来，放到一个vector数组中，然后排序，生成新链表。

空间利用率并不高（扩充了一倍的空间。）

时间利用率不高（相当于在读取了一遍链表后，重新排序了。实际上只需要一遍遍历就可以完成排序的。）
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL) return l2;
        else if(l2==NULL) return l1;
        else
        {
            vector<int> v;
            while(l2!=NULL){
                v.push_back(l2->val);
                l2=l2->next;
            }
            while(l1!=NULL){
                v.push_back(l1->val);
                l1=l1->next;
            }
            sort(v.begin(),v.end());
            ListNode *ans=new ListNode(v[0]);
            ListNode *head=ans;
            for(int i=1;i<v.size();i++){
                ListNode *k=new ListNode(v[i]);
                ans->next=k;ans=k;
            }
            return head;
        }
    }
};
```
 

# **最佳做法！！！：**

> 
<h2>**穿针引线**</h2>


 用一个针（空链表），依次穿过当前左边最小的结点。

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
         ListNode *dummy = new ListNode(-1), *cur = dummy;
        while (l1 && l2) {
            if (l1->val < l2->val) {
                cur->next = l1;
                l1 = l1->next;
            } else {
                cur->next = l2;
                l2 = l2->next;
            }
            cur = cur->next;
        }
        cur->next = l1 ? l1 : l2;
        return dummy->next;
    }
};
``` 
