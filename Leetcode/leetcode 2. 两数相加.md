# 原创：leetcode 2. 两数相加

 
![](https://img-blog.csdnimg.cn/2019042315254383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *ans=new ListNode(0);
        ListNode *t=ans;
        ListNode *p1=l1;
        ListNode *p2=l2;
        int c=0,a1=0,a2=0;
        int res;
        while(p1!=NULL||p2!=NULL)
        {
            if(p1!=NULL){
                a1=p1->val;
            }
            else a1=0;
            if(p2!=NULL){
                a2=p2->val;
            }
            else a2=0;
            res=a1+a2+c;
            if(res>=10){
                res=res-10;
                c=1;
            }
            else c=0;
            ListNode *n=new ListNode(res);
            n->val=res;
            
            t->next=n;
            t=t->next;
            if(p1!=NULL)
                p1=p1->next;
            if(p2!=NULL)
                p2=p2->next;
            
            
        }
        if(c==1)
        {
            ListNode *n=new ListNode(1);
            t->next=n;
        }
        return ans->next;
    }
};
```