### 问题描述

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[  “((()))”,  “(()())”,  “(())()”,  “()(())”,  “()()()”]

### 解决办法：递归思路

回归条件：如果左右括号都没了，那么把解返回解空间。

选择条件1：如果左括号还有，那么就递归。

递归关系：如果左括号还有，那么就用掉一个左括号（字符串+“（”，函数中left-1）

选择条件2：如果左括号剩余数量小于右括号剩余数量，那么就递归。递归关系：用掉一个右括号

### 代码

```
void backtrade(string sublist,vector<string>& res,int left,int right){
        if(left == 0 && right == 0) {
            res.push_back(sublist);
            return;
        }
        if(left>0){
            backtrade(sublist+"(",res,left-1,right);
        }
        if(left<right){
            backtrade(sublist+")",res,left,right-1);
        }
    }
    
    vector<string> generateParenthesis(int n) {      
        vector<string> res;
        backtrade("",res,n,n);
        return res;
    }
```
