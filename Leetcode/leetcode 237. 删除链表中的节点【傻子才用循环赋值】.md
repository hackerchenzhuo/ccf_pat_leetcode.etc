# 原创：leetcode 237. 删除链表中的节点【傻子才用循环赋值】

 

执行用时 : 16 ms, 在Delete Node in a Linked List的C++提交中击败了98.50% 的用户

内存消耗 : 9.4 MB, 在Delete Node in a Linked List的C++提交中击败了5.55% 的用户

**不要纠结为啥没有头结点。。。依次赋值就行。node就是要删的结点。**
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
    void deleteNode(ListNode* node) {
    ListNode*q=node->next;
    while(q->next!=NULL)
    {
        node->val=q->val;
        node=q;
        q=q->next;
    }
    node->val=q->val;
    node->next=NULL;
    }
};
```
 

**然而。。。。其实很简单**

**什么时候自己能多思考思考。。晕**

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
    //没有头结点也不需要依次赋值
    node->val=node->next->val;
    node->next=node->next->next;
    }
};
``` 

 
