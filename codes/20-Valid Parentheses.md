Given a string containing just the characters ‘(‘, ‘)’, ‘{‘, ‘}’, ‘[’ and ‘]’, determine if the input string is valid.


An input string is valid if:

- Open brackets must be closed by the same type of brackets.

- Open brackets must be closed in the correct order.

- Note that an empty string is also considered valid.


**Example 1**

  Input: “()” 
  
  Output: true


**Example 2**

  Input: “()[]{}” 

Output: true


**Example 3**

  Input: “(]”
  
  Output: false


**Example 4**

  Input: “([)]” 

Output: false


**Example 5**

  Input: “{[]}” 
  
  Output: true

### 思路

建map和stack，map中的括号互相匹配。然后遍历整个字符串，遍历的过程中，每次检查stack，如果为空，压入字符；如果栈顶字符和压入的字符匹配就弹出栈顶元素；如果栈顶字符和压入的字符不匹配就继续压入字符。

结束遍历字符串之后，如果该字符串是满足条件的字符串，现在的栈应该是空栈。

代码：

```
bool isValid(string s) {
        map<char,char> bracket={{'{','}'},{'(',')'},{'[',']'}};
        stack<char> stk;
        for(char le:s){
            if(stk.empty())
                stk.push(le);
            else if(bracket[stk.top()]==le)
                stk.pop();
            else
                stk.push(le);
        }
        if(stk.empty())
            return true;
        else
            return false;

    }
```
