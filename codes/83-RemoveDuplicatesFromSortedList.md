### 问题描述

Given a sorted linked list, delete all duplicates such that each element appear only once.  

For example, 

Given 1->1->2, return 1->2. 

Given 1->1->2->3->3, return 1->2->3. 

### 代码：

```C++
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

### JAVA

```java
public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy=head;
        while(head!=null&&head.next!=null){
            if(head.val==head.next.val)
                head.next=head.next.next;
            else
                head=head.next;
        }
        return dummy;
    }
```
