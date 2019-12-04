# 原创：leetcode 19.删除链表的倒数第N个节点【三指针一遍遍历】

执行用时 : 8 ms, 在Remove Nth Node From End of List的C++提交中击败了96.21% 的用户

内存消耗 : 8.6 MB, 在Remove Nth Node From End of List的C++提交中击败了75.76% 的用户

**需要pre，p，q三个指针。**
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        //双指针一遍扫描
        ListNode*p=head,*q=head,*pre=NULL;
        while(n)
        {
            q=q->next;
            n--;
        }
        while(q!=NULL)
        {
            pre=p;
            q=q->next;
            p=p->next;
        }
        if(pre!=NULL)
        {
            pre->next=p->next;//删除节点.
            return head;
        }
        else return head->next;
        
    }
};
```
 
