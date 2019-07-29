Design a stack that supports push, pop, top, and retrieving the minimum element in constant time. 


- push(x) – Push element x onto stack. 
- pop() – Removes the element on top of the stack. 
- top() – Get the top element. 
- getMin() – Retrieve the minimum element in the stack. 


Example:

```
  MinStack minStack = new MinStack(); 
  minStack.push(-2); 
  minStack.push(0); 
  minStack.push(-3); 
  minStack.getMin();   –> Returns -3. 
  minStack.pop(); 
  minStack.top();      –> Returns 0. 
  minStack.getMin();   –> Returns -2.
```

代码如下：

```
    stack<int>a;
    stack<int>b;

    MinStack() {   

    }

    void push(int x) {
        a.push(x);
        if(b.empty()||x<b.top())
            b.push(x);
        else
            b.push(b.top());       
    }

    void pop() {
        a.pop();
        b.pop();
    }

    int top() {
        return a.top();
    }

    int getMin() {
        return b.top();
    }
 ```

需要注意的是如果需要压入的元素没有b的栈顶元素小，也要再次把b的栈顶元素压入b栈中，这是因为要保持a和b两个栈的元素数量的一致性，防止在pop弹出的时候把a和b中的不相对应的元素弹出。
