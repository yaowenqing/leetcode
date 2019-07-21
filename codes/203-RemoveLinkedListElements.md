Remove all elements from a linked list of integers that have value val. 

**Example**


  Given: 1 –> 2 –> 6 –> 3 –> 4 –> 5 –> 6, val = 6 
  
  Return: 1 –> 2 –> 3 –> 4 –> 5 




### 解法

递归的思想

```
ListNode* removeElements(ListNode* head, int val) { 
        if (head == NULL) 
            return NULL;
        head->next = removeElements(head->next, val);
        return head->val == val ? head->next : head;
    }
```
