### 题目描述

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

- Note: For the purpose of this problem, we define empty string as valid palindrome.

**Example 1**

  Input: “A man, a plan, a canal: Panama” 
  
  Output: true

**Example 2**

  Input: “race a car” 

Output: false

### 解题思路

设置两个指针，一个从头遍历所有的alnum，另一个从尾开始遍历所有的alnum，并依次对比。

需要解释的是

```
while(isalnum(s[i])==false&&i<j)1
```

这行代码后面要求i小于j时才执行自增或者自减的运算是为了防止在中间发生j和i两个指针交换位置的情况

代码：

```
bool isPalindrome(string s) {
        for(int i=0,j=s.size()-1;i<j;i++,j--){
            while(isalnum(s[i])==false&&i<j)
                i++;
            while(isalnum(s[j])==false&&i<j)
                j--;
            if(toupper(s[i])!=toupper(s[j]))
                return false;
        }
        return true;       
    }
```
