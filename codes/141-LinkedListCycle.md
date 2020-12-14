Given a linked list, determine if it has a cycle in it.  

- Follow up：Can you solve it without using extra space? 


### 思路

这道题是快慢指针的经典应用。只需要设两个指针，一个每次走一步的慢指针和一个每次走两步的快指针，如果链表里有环的话，两个指针最终肯定会相遇。

代码：

```C++
bool hasCycle(ListNode *head) {
        ListNode*slow=head,*fast=head;
        while(fast&&fast->next){
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast)
                return true;
        }
        return false;
    }
```

JAVA:

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow=head;
        ListNode fast=head;
        while(fast!=null&&fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
            if(slow==fast)
                return true;
        }
        return false;        
    }
}
```

Go:

```go
func hasCycle(head *ListNode) bool {
    if head==nil || head.Next==nil{
        return false
    }
    slow,fast := head,head.Next
    for fast!=slow{
        if fast==nil || fast.Next==nil{
            return false
        }
        slow=slow.Next;
        fast=fast.Next.Next;
    }
    return true
}
```

