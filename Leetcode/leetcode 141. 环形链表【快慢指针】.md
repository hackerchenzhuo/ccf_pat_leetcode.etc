# 原创：leetcode 141. 环形链表【快慢指针】

刚开始都没看清题目里面的pos啥意思。。。

执行用时 : 8 ms, 在Linked List Cycle的C++提交中击败了100.00% 的用户

内存消耗 : 9.9 MB, 在Linked List Cycle的C++提交中击败了12.12% 的用户

 
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
    bool hasCycle(ListNode *head) {
        ListNode *t=head;
        if(head==NULL||head->next==NULL||head->next->next==NULL) return false;
        while(head!=NULL&&t!=NULL){
            head=head->next;
            t=t->next;
            if(t!=NULL){
                t=t->next;
            }
            else return false;
            if(head==t){
                return true;
            }
            
        }
        return false;
    }
};
```