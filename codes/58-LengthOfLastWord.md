### 问题描述

Given a string s consists of upper/lower-case alphabets and empty space characters ‘ ’, return the length of last word in the string. 

If the last word does not exist, return 0. 

Note: A word is defined as a character sequence consists of non-space characters only. 

- Example: 

  Input: “Hello World” 
  
  Output: 5


### 代码

```
 int lengthOfLastWord(string s) { 
        int len = 0, tail = s.length() - 1;
        while (tail >= 0 && s[tail] == ' ') tail--;
        while (tail >= 0 && s[tail] != ' ') {
            len++;
            tail--;
        }
        return len;
    }
```

### 解释

代码的第一个while循环是为了排除整个字符串最后的空格，因为字符串最后不一定是字母
