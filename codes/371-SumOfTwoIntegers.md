### 问题描述

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -. 

Example: 

Given a = 1 and b = 2, return 3.  


### 代码

```
int getSum(int a, int b) {
    if(b!=0)
        return getSum(a^b,(a&b)<<1);
    else
        return a;  
 }
```
