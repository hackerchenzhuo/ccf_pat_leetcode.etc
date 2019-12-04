# 原创：leetcode 234. 回文链表【最佳解】【c++】

### 回文链表最佳解：【结合了反转链表的最佳方式】

> 
<ol><li>
//快慢指针找中点
</li>
- //反转后半列表
- //依次往前遍历
</ol>

**执行用时 : 28 ms, 在Palindrome Linked List的C++提交中击败了95.77% 的用户**

**内存消耗 : 12.5 MB, 在Palindrome Linked List的C++提交中击败了77.91%的用户**

时间复杂度O（n）——————

（很重要一点，其实是O（3n），n为链表长度。还有一种方法是反转整个链表然后对比，这样子时间复杂度为O（4n），空间复杂度O（n））

空间复杂度O（1）
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
//回文链表；
//快慢指针找中点
//反转后半列表
//依次往前遍历
public:
    bool isPalindrome(ListNode* head) {
        if(!head||!head->next) return true;
        ListNode*p1=head;
        ListNode*p2=head;
        ListNode*pre=NULL;
        while(p2!=NULL&&p2->next!=NULL)
        {
            p2=p2->next->next;
            pre=p1;
            p1=p1->next;
        }
        pre->next=NULL;//截断
        ListNode*t=rev(p1);
        while(head!=NULL)
        {
            if(head->val!=t->val) return false;
            head=head->next;
            t=t->next;
        }
        
        return true;
        
        
    }
    ListNode*  rev(ListNode* p){
        ListNode*t=p;
        ListNode*pre=NULL;
        ListNode*nex=NULL;
        while(t)
        {
            nex=t->next;
            t->next=pre;
            pre=t;
            t=nex;
        }
        return pre;
    };
};
```
 
