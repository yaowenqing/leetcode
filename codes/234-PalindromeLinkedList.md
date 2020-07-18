判断链表是不是回文链表

### 解题思路

首先创建一个slow指针和fast指针，fast一次走两步直到走到链表末尾，slow一次走一步。这样的目的是使slow指向链表最中间，从而得到链表最中间的位置（如果链表结点为偶数个，指向中间靠前的节点）。 

获得链表中间的位置之后，反转这个位置之后的所有节点。然后分别从头结点和slow节点下一个节点开始（终止条件为后面的slow指针指向的位置为NULL），依次比较节点中的值是否一样。如果全部一样，说明这是一个回文链表。 

例如对于 1 2 3 4 3 2 1 

slow指针会指向4这个节点，反转之后为1 2 3 4 1 2 3，此时slow节点下一个节点为1，依次对比1和1,2和2,3和3。全部一样，说明这是一个回文链表。终止条件由slow指针决定，是因为在这种情况下就不会考虑head所指的下一个数字4了（它是什么已经没有关系了）


```C++
bool isPalindrome(ListNode* head) {
        if(head==NULL||head->next==NULL)
            return true;
        ListNode* slow=head;
        ListNode* fast=head;
        while(fast->next!=NULL&&fast->next->next!=NULL){
            slow=slow->next;
            fast=fast->next->next;
        }
        slow->next=reverseList(slow->next);
        slow=slow->next;
        while(slow!=NULL){
            if(head->val!=slow->val)
                return false;
            head=head->next;
            slow=slow->next;
        }
        return true;
    }
    ListNode* reverseList(ListNode* head) {
        ListNode* pre=NULL;
        ListNode* next=NULL;
        while(head!=NULL){
            next=head->next;
            head->next=pre;
            pre=head;
            head=next;
        }
        return pre;
    }
    
```

另一种方法：


```C++
class Solution {
public:
    ListNode*temp;
    bool isPalindrome(ListNode* head) {
        temp = head;
        return check(head);
    }
    bool check(ListNode* p) {
        if (NULL == p) return true;
        bool isPal = check(p->next) & (temp->val == p->val);
        temp = temp->next;
        return isPal;
    }

};
```

Java版本：
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head==null || head.next==null)
            return true;
        ListNode slow=head;
        ListNode fast=head;
        while(fast.next!=null && fast.next.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        slow.next=reverse(slow.next);
        slow=slow.next;
        while(slow!=null){
            if(head.val!=slow.val)
                return false;
            head=head.next;
            slow=slow.next;
        }
        return true;
    }
    public ListNode reverse(ListNode head){
        ListNode pre=null;
        ListNode next=null;
        while(head!=null){
            next=head.next;
            head.next=pre;
            pre=head;
            head=next;
        }
        return pre;
    }
}
```
