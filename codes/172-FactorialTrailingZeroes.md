### 问题描述

Given an integer n, return the number of trailing zeroes in n!.

Example 1:


  Input: 3 
  
  Output: 0 
  
  Explanation: 3! = 6, no trailing zero.


Example 2:


  Input: 5 
  
  Output: 1 
  
  Explanation: 5! = 120, one trailing zero.


- Note: Your solution should be in logarithmic time complexity.

### 代码

我的思路，先判断它是5的多少次方级别的数字，比如129大于125小于625，属于5的3次方级别的数字。然后再用一个 for循环分别除以5，25，125，最后结果相加。代码如下:


```
int trailingZeroes(int n) {
        if(n<5)
            return 0;
        int res=0,i=0,temp=n;

        while(temp>=5){
            temp=temp/5;
            i++;
        }

        for(int k=1;k<=i;k++){
            int m=pow(5,k);           
            res+=n/m;
        }
        return res;
    }
```

然后我把自己的代码优化一下，去掉是5的多少次方级别数字的这一判断过程：


```
int trailingZeroes(int n) {
        int res = 0;
        while (n >= 5){
            res += n / 5;
            n = n / 5;
        }
        return res;
    }
```

网上看到别人的优雅递归解法：

```

 int trailingZeroes(int n) {
        return n == 0 ? 0 : n / 5 + trailingZeroes(n / 5);
    }
```
