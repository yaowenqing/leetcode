Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

Example:

```
MyStack stack = new MyStack();
stack.push(1);
stack.push(2);
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```

>Notes:You must use only standard operations of a queue – which means only push to back, peek/pop from front, size, and is empty operations are valid.
Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

### 思路

每往队列中插入一个元素，都将它前面的元素弹出并重新插入队列中，这样就能保证最后插入队列的元素始终在队列的最前端，比如插入a,b,c,d这四个元素，队列中元素的顺序依次为a,ab,abc,abcd，这样插入的时间复杂度是O(n)，弹出和获取最后一个元素的时间复杂度是O(1)

![](https://github.com/yaowenqing/leetcode/blob/master/images/3.png)

代码如下：

```
class MyStack {
 
private:
    queue<int> q;
    int size;
  
public:
    MyStack() {
        size=0;
    }
  
  /** Push element x onto stack. */
    void push(int x) {
       	if(q.size() == 0) {
       	    q.push(x);
   	}
   	else {
  	    q.push(x);
   	    for(int i=0; i<size; i++) {
     		q.push(q.front());
     		q.pop();
    	    }
 	}
   	size++;
    }
  
  /** Removes the element on top of the stack and returns that element. */
    int pop() {
   	int ret = q.front();
   	q.pop();
      	return ret;
    }
  
  /** Get the top element. */
    int top() {
        return q.front();
    }
  
  /** Returns whether the stack is empty. */
    bool empty() {
      return q.size() == 0;
    }
};
```
