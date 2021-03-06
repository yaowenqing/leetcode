Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example: 


  Input: 1->2->4, 1->3->4 
  
  Output: 1->1->2->3->4->4


最朴素的方法：

```C++
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode*dummy = new ListNode(-1);
        ListNode*cur=dummy;
        while(l1&&l2){
            if(l1->val<=l2->val){
                cur->next=l1;
                l1=l1->next;
            }else{
                cur->next=l2;
                l2=l2->next;
            }
            cur=cur->next;
        }
        cur->next=l1?l1:l2;
        return dummy->next;                
    }
```

Java版本的解法：
```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {        
        ListNode dummy=new ListNode(-1);
        ListNode cur=dummy;
        while(l1!=null&&l2!=null){
            if(l1.val<=l2.val){
                cur.next=l1;
                l1=l1.next;
            }else{
                cur.next=l2;
                l2=l2.next;
            }
            cur=cur.next;
        }
        cur.next=l1!=null?l1:l2;
        return dummy.next;   
    }
}
```


递归解法(C++)：

```C++
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1)
            return l2;
        if(!l2)
            return l1;
        if(l1->val<=l2->val){
            l1->next=mergeTwoLists(l1->next,l2);
            return l1;
        }else{
            l2->next=mergeTwoLists(l1,l2->next);
            return l2;
        }
    }
```
