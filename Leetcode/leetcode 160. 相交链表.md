# 原创：leetcode 160. 相交链表

 easy,知识迁移即可。双指针。找规律。

若有相交后半截必定重合。

执行用时 : 68 ms, 在Intersection of Two Linked Lists的C++提交中击败了95.19% 的用户

内存消耗 : 16.6 MB, 在Intersection of Two Linked Lists的C++提交中击败了64.61% 的用户

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
//若有相交，后半截必定重合
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        //先确定长度
        ListNode *t1=headA;
        ListNode *t2=headB;
        int l1=0,l2=0;
        while(t1!=NULL){
            t1=t1->next;l1++;
        }
        while(t2!=NULL){
            t2=t2->next;l2++;
        }
        int cha=l1-l2;
        ListNode *k2=headA;
        ListNode *k1=headB;
        if(cha>0){//前面的长
            k1=headA;
            k2=headB;
        }
        else {
            cha=-cha;
        }
        while(cha>0){
            k1=k1->next;
            cha--;
        }
        while(k1!=NULL){
            if(k1==k2)return k1;
            k1=k1->next;
            k2=k2->next;
        }
        return NULL;
        
        
    }
};
``` 
