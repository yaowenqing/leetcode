Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.
 
**Example**

Given 1->2->3->4, you should return the list as 2->1->4->3.

### 思路

递归的方法

```
ListNode* swapPairs(ListNode* head) {
        if(head==NULL||head->next==NULL)
            return head;
        swapPairs(head->next->next);
        swap(head->val,head->next->val);
        return head;
}
```
