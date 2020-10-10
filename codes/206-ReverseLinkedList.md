```C++
ListNode* reverseList(ListNode* head) {
        ListNode*temp=NULL,*nextNode=NULL;
        while(head){
            nextNode=head->next;
            head->next=temp;
            temp=head;
            head=nextNode;
        }
        return temp;
    }
```

Java:
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode temp=null,nextNode=null;
        while(head!=null){
            nextNode=head.next;
            head.next=temp;
            temp=head;
            head=nextNode;
        }
        return temp;
    }
}
```
