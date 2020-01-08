# TASK02
链表相关
===
1. 合并两个有序链表
---
https://leetcode-cn.com/problems/merge-two-sorted-lists/

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* last;
    struct ListNode* newlist  = last = NULL;
    if(l1==NULL) return l2;
    if(l2==NULL) return l1;
        while(l1 && l2)
        {
            struct ListNode* current = (struct ListNode*)malloc(sizeof (struct ListNode));
            if(l1 -> val >= l2 -> val)
            {
                current -> val = l2 -> val; 
                l2 = l2 -> next;
            }
            else
            {
                current -> val = l1 -> val;
                l1 = l1 -> next;
            }
            current -> next = NULL;
            if(newlist == NULL)
                newlist = current;
            else
                last -> next = current;
            last = current;
        }
        while(l1)
        {
            struct ListNode* current = (struct ListNode*)malloc(sizeof (struct ListNode));
            current -> val = l1 -> val;
            current -> next = NULL;
            if(last)
            last -> next = current;
            last = current;
            l1 = l1 -> next;
        }
        while(l2)
        {
            struct ListNode* current = (struct ListNode*)malloc(sizeof (struct ListNode));
            current -> val = l2 -> val;
            current -> next = NULL;
            if(last) 
            last -> next = current;
            last = current;
            l2 = l2 -> next;
        }
        return newlist;
}
```
2. 删除链表的倒数第N个节点
---

https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
        struct ListNode *dummy = (struct ListNode*)malloc(sizeof(struct ListNode));
        dummy->val = 0;
        dummy->next = head;
        
        struct ListNode *fast, *low;
        fast = low = dummy;
        while(n > 0){
                fast = fast->next;      
                n--;
        }
        while(fast->next != NULL){
                low = low->next;
                fast = fast->next;
        }
        
        low->next = low->next->next;
        
        return dummy->next;
        
}
```

3. 旋转链表
---

https://leetcode-cn.com/problems/rotate-list/

给定一个链表，旋转链表，将链表每个节点向右移动k个位置，其中k是非负数。

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* rotateRight(struct ListNode* head, int k)
{
    struct ListNode *p;
    struct ListNode *q;
    p=(struct ListNode*)malloc(sizeof(struct ListNode));
    q=(struct ListNode*)malloc(sizeof(struct ListNode));

    int n=1;
    int m=1;
    int l;
    p=head;
   
    if (head==NULL||k==0) return head;
    while(head->next!=NULL)
    {
        head=head->next;
        m++;
    }
    head->next=p;
    l=m-k%m;
    for(;n<l;n++)
    {
        p=p->next;
    }
    q=p->next;
    p->next=NULL;

return q;
}
```
