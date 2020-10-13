Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.
 
**Example**

Given 1->2->3->4, you should return the list as 2->1->4->3.

### 思路

递归的方法

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head==null||head.next==null)   
            return head;
        ListNode temp=head.next;
        head.next=swapPairs(head.next.next);
        temp.next=head;
        return temp;
    }
}
```

迭代方法

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy=new ListNode(0);
        dummy.next=head;
        ListNode temp=dummy;
        while(temp.next!=null && temp.next.next!=null){
            ListNode node1=temp.next;
            ListNode node2=temp.next.next;
            temp.next=node2;
            node1.next=node2.next;
            node2.next=node1;
            temp=node1;
        }
        return dummy.next;
    }
}
```

