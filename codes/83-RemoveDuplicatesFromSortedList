### 问题描述

Given a sorted linked list, delete all duplicates such that each element appear only once.  

For example, 

Given 1->1->2, return 1->2. 

Given 1->1->2->3->3, return 1->2->3. 

### 代码：(21ms版本)

```
ListNode* deleteDuplicates(ListNode* head) {
        ListNode*cur=head;
        while(cur!=NULL&&cur->next!=NULL){
            if(cur->next->val==cur->val)
                cur->next=cur->next->next;
            else
                cur=cur->next;
        }
        return head;
    }
```

稍微改一改可以快8ms：（13ms版本）

```
ListNode* deleteDuplicates(ListNode* head) {
        ListNode* cur=head;
        while(cur && cur->next){
            if(cur->val==cur->next->val){
                cur->next=cur->next->next;
            }
            else
                cur=cur->next;
        }
        return head;
    }
```

这启发我，在处理大部分链表问题，写while判断条件的时候，最好写成类似

> while(cur && cur->next)

的形式，而不是

>while(cur!=NULL && cur->next!=NULL)

的形式。
