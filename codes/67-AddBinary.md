### 问题描述

Given two binary strings, return their sum (also a binary string). 

The input strings are both non-empty and contains only characters 1 or 0. 

**Example 1**

  Input: a = “11”, b = “1”
  
  Output: “100”


**Example 2**

  Input: a = “1010”, b = “1011” 
  
  Output: “10101”


### 思路

用两个指针分别指向a和b的末尾，然后每次取出一个字符，转为数字，若无法取出字符则按0处理，然后定义进位offset，初始化为0，将三者加起来，对2取余即为当前位的数字，对2取商即为当前进位的值，最后整个while循环结束之后还要判断下offset，如果为1的话，要在结果最前面加上一个1，代码如下：

```
string addBinary(string a, string b) {
        string res="";
        int n1=a.size()-1,n2=b.size()-1;
        int offset=0;
        while(n1>=0||n2>=0){
            int m=n1>=0?a[n1--]-'0':0;
            int n=n2>=0?b[n2--]-'0':0;
            int num=m+n+offset;
            offset=num/2;
            res=char(num%2+'0')+res;
        }

        return offset==1? "1"+res:res;

    }
```
