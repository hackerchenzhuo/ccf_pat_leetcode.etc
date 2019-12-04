# 原创：leetcode 148. 排序链表【链表的归并排序】

**在 **O**(**n** log **n**) 时间复杂度和常数级空间复杂度下，对链表进行排序。**

执行用时 :60 ms, 在所有C++提交中击败了98.21%的用户

内存消耗 :13 MB, 在所有C++提交中击败了43.42%的用户

技巧：看见nlogn的排序算法：归并排序 和 快排。又因为是链表，快排可能不行，所以要用归并。

●对链表进行归并的思路：

关键：需要及时断开链表成两部分，一直递归知道最后元素为1 or 0个才停止。

最后一层一层归并，每一层左右两边都是有序的。

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
    ListNode* sortList(ListNode* head) {
        //归并排序->中间时刻需要断裂键值
        //快慢指针
        //
        return mergesort(head);
    }
    ListNode* mergesort(ListNode* head) 
    {
        if(head==NULL||head->next==NULL) return head;//递归终点只有一个元素或者没有元素了
        ListNode* mid=head;
        ListNode* fast=head;
        ListNode* slow=head;
        while(fast!=NULL&&fast->next!=NULL)
        {
            fast=fast->next->next;
            mid=slow;
            slow=slow->next;
        }
        mid->next=NULL;//左边部分的终点处断开
        ListNode*p1=mergesort(head);
        ListNode*p2=mergesort(slow);
        return merge(p1,p2);
        
    }
    
     ListNode*merge(ListNode* p1,ListNode* p2)
     {
         if(p1==NULL)
         {
             return p2;
         }
         if(p2==NULL)
         {
             return p1;
         }
         if(p1->val<=p2->val)
         {
             p1->next=merge(p1->next,p2);
             return p1;
         }
         else
         {
             p2->next=merge(p1,p2->next);
             return p2;
         }
     }
};
``` 

 

 
