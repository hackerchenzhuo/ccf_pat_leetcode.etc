# 原创：leetcode 206. 反转链表

 

执行用时 : 16 ms, 在Reverse Linked List的C++提交中击败了96.25% 的用户

内存消耗 : 9.1 MB, 在Reverse Linked List的C++提交中击败了53.22% 的用户

 

前，中，后指针，一次遍历反转列表。

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
    ListNode* reverseList(ListNode* head) {
        if(head==NULL||head->next==NULL) return head;
        ListNode* pre=head;
        ListNode* p=head->next;
        ListNode* lat=p->next;
        head->next=NULL;
        p->next=pre;
        while(lat!=NULL){
            p->next=pre;
            pre=p;
            p=lat;
            lat=lat->next;
        }
        p->next=pre;
        return p;
        
        
        
    }
};
```

参考答案（比我的更清楚，没有冗余）

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
    ListNode* reverseList(ListNode* head) {
      
       
        if(head==nullptr){
            return head;
        }
        
        ListNode* curr=head;
        ListNode* nex=nullptr;
        ListNode* prev=nullptr;
        
        
        while(curr){
            nex = curr->next;
            curr->next = prev;
            prev=curr;
            curr=nex;
        }
        head=prev;
        
        return head;
        
    }
  
};
``` 
